Command necessary:

docker-compose -f docker.elasticsearch.yaml up

curl -XPUT http://localhost:9200/try-0001

curl -XPUT -H "Content-Type: application/json" http://localhost:9200/try-0001/_doc/10 -d '
{
	"array" : ["1","2"]
}
'

curl -XPOST -H "Content-Type: application/json" http://localhost:9200/try-0001/_doc/10/_update -d '
{
	"script": {
		"lang": "painless",
		"source": "if (ctx._source.array==null) {ctx._source.array=[params.new_array]}else{ctx._source.annotation.add(params.new_array)}",
		"params" :{"new_array":"34"}
	}
}'
