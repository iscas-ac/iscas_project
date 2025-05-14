# 软件图谱ElasticSearch数据说明

## 1. ES容器信息
使用docker单点部署ES  ，容器信息如下:  
(1)线上版

|所在服务器|CONTAINER ID|IMAGE|NAME|PORTS|登录信息|   
|---|---|---|---|---|---|
|sec-srv10(192.168.59.201)|6329f20badce|elasticsearch:7.17.14|es_softgraph|0.0.0.0:9210->9200/tcp, :::9210->9200/tcp, 0.0.0.0:9310->9300/tcp, :::9310->9300/tcp|username='elastic'<br/>password='iscas139'|

(2) 测试版  

|所在服务器|CONTAINER ID|IMAGE|NAME|PORTS|登录信息|   
|---|---|---|---|---|---|
|sec-srv10(192.168.59.201)|8ee1e37d8e5d|elasticsearch:7.17.14|es_softgraph_test|0.0.0.0:9220->9200/tcp, :::9220->9200/tcp, 0.0.0.0:9320->9300/tcp, :::9320->9300/tcp|username='elastic'<br/>password='iscas139'|


## 2. 数据查询说明
### 2.1 字段说明 
字段基本与neo4j中的一致，仅将驼峰命名改为下划线命名。  
有两个字段有变化：  
- neo4j中的'version'对应es中的'ver'；  
- neo4j中的'pypiID'、'oepkgsID'对应es中的'source_id'。    

因此，详细说明也可参考neo4j的实体属性说明文件：*SoftGraph Schema/SoftGraph_v3.1/neo4j schema/SoftGraph_实体属性(neo4j)_v3.1.docx*
<table>
	<tr>
	    <th>Index</th>
	    <th>字段</th>
	    <th>字段说明</th>
        <th>mappings</th>
	</tr >
	<tr>
	    <td rowspan="27">repository</td>
	    <td>name</td>
	    <td>仓库名称</td>  
        <td rowspan="27">
        <pre>
        {
          "repository" : {
            "mappings" : {
              "properties" : {
                "commit_num" : {
                  "type" : "integer"
                },
                "contributor_num" : {
                  "type" : "integer"
                },
                "country" : {
                  "type" : "keyword"
                },
                "created_at" : {
                  "type" : "date",
                  "format" : "epoch_second"
                },
                "deleted_time" : {
                  "type" : "date",
                  "format" : "epoch_second"
                },
                "description" : {
                  "type" : "text",
                  "analyzer" : "ik_max_word",
                  "search_analyzer" : "ik_smart"
                },
                "file_path" : {
                  "type" : "keyword"
                },
                "file_soft_link" : {
                  "type" : "keyword"
                },
                "fork_num" : {
                  "type" : "integer"
                },
                "full_name" : {
                  "type" : "text",
                  "fields" : {
                    "keyword" : {
                      "type" : "keyword",
                      "ignore_above" : 256
                    }
                  },
                  "analyzer" : "ik_max_word",
                  "search_analyzer" : "ik_smart"
                },
                "insert_time" : {
                  "type" : "date",
                  "format" : "epoch_second"
                },
                "is_supply" : {
                  "type" : "boolean"
                },
                "issue_num" : {
                  "type" : "integer"
                },
                "language" : {
                  "type" : "keyword"
                },
                "last_30_days_commit_num" : {
                  "type" : "integer"
                },
                "last_year_commit_num" : {
                  "type" : "integer"
                },
                "latest_commit_time" : {
                  "type" : "date",
                  "format" : "epoch_second"
                },
                "name" : {
                  "type" : "text",
                  "fields" : {
                    "keyword" : {
                      "type" : "keyword",
                      "ignore_above" : 256
                    }
                  },
                  "analyzer" : "ik_max_word",
                  "search_analyzer" : "ik_smart"
                },
                "pull_request_num" : {
                  "type" : "integer"
                },
                "release_num" : {
                  "type" : "integer"
                },
                "size" : {
                  "type" : "long"
                },
                "source" : {
                  "type" : "keyword"
                },
                "source_id" : {
                  "type" : "integer"
                },
                "star_num" : {
                  "type" : "integer"
                },
                "update_time" : {
                  "type" : "date",
                  "format" : "epoch_second"
                },
                "url" : {
                  "type" : "keyword"
                },
                "watch_num" : {
                  "type" : "integer"
                }
              }
            }
          }
        }
        </pre>
        </td>
	</tr >
	<tr >
	    <td >full_name</td>
	    <td >仓库全名。例如，“https://github.com/edgexfoundry/edgex-go”中的“edgexfoundry/edgex-go”即为仓库全名。</td>
	</tr>
	<tr>
	    <td >description</td>
	    <td >仓库描述</td>
	</tr>
	<tr>
	    <td >contributor_num</td>
	    <td >贡献者数量</td>
	</tr>
	<tr>
	    <td >star_num</td>
	    <td >star数量</td>
	</tr>
	<tr>
	    <td >fork_num</td>
	    <td >fork数量</td>
	</tr>
	<tr>
	    <td >issue_num</td>
	    <td >issue数量</td>
	</tr>
	<tr>
	    <td >watch_num</td>
	    <td >watch数量</td>
	</tr>
    <tr>
	    <td >pull_request_num</td>
	    <td >pr数量</td>
	</tr>
    <tr>
	    <td >release_num</td>
	    <td >仓库tag数量</td>
	</tr>
    <tr>
	    <td >url</td>
	    <td >仓库url</td>
	</tr>
    <tr>
	    <td >commit_num</td>
	    <td >仓库commit数量</td>
	</tr>
    <tr>
	    <td >last_year_commit_num</td>
	    <td >近一年commit数量</td>
	</tr>
    <tr>
	    <td >last_30_days_commit_num</td>
	    <td >近一个月commit数量</td>
	</tr>
    <tr>
	    <td >latest_commit_time</td>
	    <td >最近一次commit时间</td>
	</tr>
    <tr>
	    <td >is_supply</td>
	    <td >是否仍在供应</td>
	</tr>
    <tr>
	    <td >deleted_time</td>
	    <td >删库时间</td>
	</tr>
    <tr>
	    <td >created_at</td>
	    <td >仓库创建时间</td>
	</tr>
    <tr>
	    <td >language</td>
	    <td >编程语言</td>
	</tr>
    <tr>
	    <td >country</td>
	    <td >仓库所属国家</td>
	</tr>
    <tr>
	    <td >size</td>
	    <td >仓库大小（KB）</td>
	</tr>
    <tr>
	    <td >source</td>
	    <td >仓库来源/平台，如github等</td>
	</tr>    
    <tr>
	    <td >source_id</td>
	    <td >仓库在原托管平台上的ID</td>
	</tr>
    <tr>
	    <td >file_path</td>
	    <td >仓库源码在服务器上的路径</td>
	</tr>
    <tr>
	    <td >file_soft_link</td>
	    <td >仓库源码软链接</td>
	</tr>
    <tr>
	    <td >insert_time</td>
	    <td >数据插入时间</td>
	</tr>
    <tr>
	    <td >update_time</td>
	    <td >数据更新时间</td>
	</tr>
    <tr>
	    <td rowspan="37">software</td>
	    <td>alias</td>
	    <td>软件别名</td>  
        <td rowspan="37">
        <pre>
        {
          "software" : {
            "mappings" : {
              "properties" : {
                "alias" : {
                  "type" : "text",
                  "analyzer" : "ik_max_word",
                  "search_analyzer" : "ik_smart"
                },
                "category" : {
                  "type" : "text",
                  "analyzer" : "ik_max_word",
                  "search_analyzer" : "ik_smart"
                },
                "country" : {
                  "type" : "keyword"
                },
                "description" : {
                  "type" : "text",
                  "analyzer" : "ik_max_word",
                  "search_analyzer" : "ik_smart"
                },
                "download_url" : {
                  "type" : "keyword"
                },
                "essential" : {
                  "type" : "boolean"
                },
                "file_path" : {
                  "type" : "keyword"
                },
                "homepage" : {
                  "type" : "keyword"
                },
                "insert_time" : {
                  "type" : "date",
                  "format" : "epoch_second"
                },
                "is_binary" : {
                  "type" : "boolean"
                },
                "is_latest_version" : {
                  "type" : "boolean"
                },
                "is_open_source" : {
                  "type" : "boolean"
                },
                "label" : {
                  "type" : "text",
                  "analyzer" : "ik_max_word",
                  "search_analyzer" : "ik_smart"
                },
                "language" : {
                  "type" : "keyword"
                },
                "license_category" : {
                  "type" : "keyword"
                },
                "main_module" : {
                  "type" : "keyword"
                },
                "modified_num" : {
                  "type" : "integer"
                },
                "name" : {
                  "type" : "text",
                  "fields" : {
                    "keyword" : {
                      "type" : "keyword",
                      "ignore_above" : 256
                    }
                  },
                  "analyzer" : "ik_max_word",
                  "search_analyzer" : "ik_smart"
                },
                "name_version" : {
                  "type" : "keyword"
                },
                "priority" : {
                  "type" : "keyword"
                },
                "provide" : {
                  "type" : "text",
                  "analyzer" : "ik_max_word",
                  "search_analyzer" : "ik_smart"
                },
                "published_time" : {
                  "type" : "date",
                  "format" : "epoch_second"
                },
                "purl" : {
                  "type" : "keyword"
                },
                "release" : {
                  "type" : "keyword"
                },
                "repo_id" : {
                  "type" : "integer"
                },
                "section" : {
                  "type" : "keyword"
                },
                "size" : {
                  "type" : "long"
                },
                "source" : {
                  "type" : "keyword"
                },
                "source_id" : {
                  "type" : "keyword"
                },
                "summary" : {
                  "type" : "text",
                  "analyzer" : "ik_max_word",
                  "search_analyzer" : "ik_smart"
                },
                "update_time" : {
                  "type" : "date",
                  "format" : "epoch_second"
                },
                "vendor" : {
                  "type" : "keyword"
                },
                "ver" : {
                  "type" : "keyword"
                },
                "version_release" : {
                  "type" : "keyword"
                },
                "virtual" : {
                  "type" : "boolean"
                }
              }
            }
          }
        }
        </pre>
        </td>
	</tr >
	<tr >
	    <td >category</td>
	    <td >软件类型，如“operating system”等。（如有多个值，逗号分隔）</td>
	</tr>
    <tr >
	    <td >country</td>
	    <td >国籍</td>
	</tr>
    <tr >
	    <td >description</td>
	    <td >描述</td>
	</tr>
    <tr >
	    <td >download_url</td>
	    <td >软件包下载链接</td>
	</tr>
    <tr >
	    <td >essential</td>
	    <td >是否是（debian/ubuntu）操作系统必备的软件</td>
	</tr>
    <tr >
	    <td >file_path</td>
	    <td >软件包文件在服务器上的路径</td>
	</tr>
    <tr >
	    <td >homepage</td>
	    <td >软件官网url</td>
	</tr>
    <tr >
	    <td >insert_time</td>
	    <td >该条数据入库时间</td>
	</tr>
    <tr >
	    <td >is_binary</td>
	    <td >是否为二进制包</td>
	</tr>
    <tr >
	    <td >is_latest_version</td>
	    <td >是否是最新版本</td>
	</tr>
    <tr >
	    <td >is_open_source</td>
	    <td >是否开源</td>
	</tr>
    <tr >
	    <td >label</td>
	    <td >标签（如有多个值，逗号分隔）</td>
	</tr>
    <tr >
	    <td >language</td>
	    <td >编程语言</td>
	</tr>
    <tr >
	    <td >license_category</td>
	    <td >许可证类型</td>
	</tr>
    <tr >
	    <td >main_module</td>
	    <td >cpan软件包的主模块</td>
	</tr>
    <tr >
	    <td >modified_num</td>
	    <td >该条数据调整的次数。主要用于数据存储使用，便于后续删除存错的数据</td>
	</tr>
    <tr >
	    <td >name</td>
	    <td >软件名称</td>
	</tr>
    <tr >
	    <td >name_version</td>
	    <td >“name@version”形式</td>
	</tr>
    <tr >
	    <td >priority</td>
	    <td >deb）软件包的重要程度，可以取值：required, important, standard, optional, extra。详见https://www.debian.org/doc/debian-policy/ch-archive.html#s-priorities</td>
	</tr>
    <tr >
	    <td >provide</td>
	    <td >cpan软件包中的所有模块，空格分隔</td>
	</tr>
    <tr >
	    <td >published_time</td>
	    <td >产品的发布时间</td>
	</tr>
    <tr >
	    <td >purl</td>
	    <td >软件的purl （package URL）</td>
	</tr>
    <tr >
	    <td >release</td>
	    <td >当前版本发布次数，如“1.2.0-1”中的“1”（主要适用于rpm和deb包）</td>
	</tr>
    <tr >
	    <td >repo_id</td>
	    <td >软件包的仓库的ID</td>
	</tr>
    <tr >
	    <td >section</td>
	    <td >（deb）软件包的类别</td>
	</tr>
    <tr >
	    <td >size</td>
	    <td >软件包大小（KB）</td>
	</tr>
    <tr >
	    <td >source</td>
	    <td >软件包来源。（如有多个值，逗号分隔）</td>
	</tr>
    <tr >
	    <td >source_id</td>
	    <td >软件包来源ID</td>
	</tr>
    <tr >
	    <td >summary</td>
	    <td >产品的简短描述</td>
	</tr>
    <tr >
	    <td >update_time</td>
	    <td >该条数据更新时间</td>
	</tr>
    <tr >
	    <td >vendor</td>
	    <td >软件包厂商/主要维护开发者/owner</td>
	</tr>
    <tr >
	    <td >ver</td>
	    <td >软件版本</td>
	</tr>
    <tr >
	    <td >version_release</td>
	    <td >“version-release[.dist_tag]”如“1.2.0-1”、“1.3.1-1.oe1”（主要适用于rpm和deb包）</td>
	</tr>
    <tr >
	    <td >file_list</td>
      <td >软件包含有文件信息的列表，包括文件名、文件大小和文件路径</td>
	</tr>
    <tr >
	    <td >parent_purl</td>
      <td >上一级软件包的purl</td>
	</tr>
    <tr >
	    <td >virtual</td>
	    <td >是否是虚拟节点</td>
	</tr>
	<tr>
	    <td rowspan="15">dataset</td>
	    <td>alias</td>
	    <td>别名</td>  
        <td rowspan="15">
        <pre>
        {
          "dataset" : {
            "mappings" : {
              "properties" : {
                "alias" : {
                  "type" : "text",
                  "analyzer" : "ik_max_word",
                  "search_analyzer" : "ik_smart"
                },
                "created_at" : {
                  "type" : "date",
                  "format" : "epoch_second"
                },
                "last_modified" : {
                  "type" : "date",
                  "format" : "epoch_second"
                },
                "description" : {
                  "type" : "text",
                  "analyzer" : "ik_max_word",
                  "search_analyzer" : "ik_smart"
                },
                "full_name" : {
                  "type" : "text",
                  "fields" : {
                    "keyword" : {
                      "type" : "keyword",
                      "ignore_above" : 256
                    }
                  },
                  "analyzer" : "ik_max_word",
                  "search_analyzer" : "ik_smart"
                },
                "insert_time" : {
                  "type" : "date",
                  "format" : "epoch_second"
                },
                 "name" : {
                  "type" : "text",
                  "fields" : {
                    "keyword" : {
                      "type" : "keyword",
                      "ignore_above" : 256
                    }
                  },
                  "analyzer" : "ik_max_word",
                  "search_analyzer" : "ik_smart"
                },
                "size" : {
                    "type" : "long"
                },
                "source" : {
                    "type" : "keyword"
                },
                "update_time" : {
                      "type" : "date",
                      "format" : "epoch_second"
                },
                "label": {
                    "type": "text",
                    "analyzer": "ik_max_word",
                    "search_analyzer": "ik_smart"
                },
                "vendor": {
                    "type": "keyword"
                },
                "downloads": {
                    "type": "integer"
                },
                "likes": {
                    "type": "integer"
                }
              }
            }
          }
        }
        </pre>
        </td>
	</tr>
    <tr>
	    <td >name</td>
	    <td >名称</td>
	</tr>
	<tr>
	    <td >label</td>
	    <td >标签（如有多个值，逗号分隔）</td>
	</tr>
	<tr>
	    <td >vendor</td>
	    <td >开发者</td>
	</tr>
	<tr>
	    <td >full_name</td>
	    <td >全名</td>
	</tr>
    <tr>
	    <td >description</td>
	    <td >描述</td>
	</tr>
	<tr>
	    <td >downloads</td>
	    <td >下载数量</td>
	</tr>
	<tr>
	    <td >likes</td>
	    <td >likes数量</td>
	</tr>
	<tr>
	    <td >s3URL</td>
	    <td >下载地址</td>
	</tr>
	<tr >
	    <td >created_at</td>
	    <td >创建时间</td>
	</tr>
	<tr>
	    <td >last_modified</td>
	    <td >最近修改时间</td>
	</tr>
    <tr>
	    <td >insert_time</td>
	    <td >该条数据入库时间</td>
	</tr>
	<tr>
	    <td >update_time</td>
	    <td >该条数据更新时间</td>
	</tr>
    <tr>
	    <td >size</td>
	    <td >软件包大小（KB）</td>
	</tr>
    <tr>
	    <td >source</td>
	    <td >来源</td>
	</tr>
	<tr>
	    <td rowspan="15">model</td>
	    <td>alias</td>
	    <td>别名</td>  
        <td rowspan="15">
        <pre>
        {
          "model" : {
            "mappings" : {
              "properties" : {
                "alias" : {
                  "type" : "text",
                  "analyzer" : "ik_max_word",
                  "search_analyzer" : "ik_smart"
                },
                "created_at" : {
                  "type" : "date",
                  "format" : "epoch_second"
                },
                "last_modified" : {
                  "type" : "date",
                  "format" : "epoch_second"
                },
                "description" : {
                  "type" : "text",
                  "analyzer" : "ik_max_word",
                  "search_analyzer" : "ik_smart"
                },
                "full_name" : {
                  "type" : "text",
                  "fields" : {
                    "keyword" : {
                      "type" : "keyword",
                      "ignore_above" : 256
                    }
                  },
                  "analyzer" : "ik_max_word",
                  "search_analyzer" : "ik_smart"
                },
                "insert_time" : {
                  "type" : "date",
                  "format" : "epoch_second"
                },
                 "name" : {
                  "type" : "text",
                  "fields" : {
                    "keyword" : {
                      "type" : "keyword",
                      "ignore_above" : 256
                    }
                  },
                  "analyzer" : "ik_max_word",
                  "search_analyzer" : "ik_smart"
                },
                "size" : {
                    "type" : "long"
                },
                "source" : {
                    "type" : "keyword"
                },
                "update_time" : {
                      "type" : "date",
                      "format" : "epoch_second"
                },
                "label": {
                    "type": "text",
                    "analyzer": "ik_max_word",
                    "search_analyzer": "ik_smart"
                },
                "vendor": {
                    "type": "keyword"
                },
                "downloads": {
                    "type": "integer"
                },
                "likes": {
                    "type": "integer"
                }
              }
            }
          }
        }
        </pre>
        </td>
	</tr>
    <tr>
	    <td >name</td>
	    <td >名称</td>
	</tr>
	<tr>
	    <td >label</td>
	    <td >标签（如有多个值，逗号分隔）</td>
	</tr>
	<tr>
	    <td >vendor</td>
	    <td >开发者</td>
	</tr>
	<tr>
	    <td >full_name</td>
	    <td >全名</td>
	</tr>
    <tr>
	    <td >description</td>
	    <td >描述</td>
	</tr>
	<tr>
	    <td >downloads</td>
	    <td >下载数量</td>
	</tr>
	<tr>
	    <td >likes</td>
	    <td >likes数量</td>
	</tr>
	<tr>
	    <td >s3URL</td>
	    <td >下载地址</td>
	</tr>
	<tr >
	    <td >created_at</td>
	    <td >创建时间</td>
	</tr>
	<tr>
	    <td >last_modified</td>
	    <td >最近修改时间</td>
	</tr>
    <tr>
	    <td >insert_time</td>
	    <td >该条数据入库时间</td>
	</tr>
	<tr>
	    <td >update_time</td>
	    <td >该条数据更新时间</td>
	</tr>
    <tr>
	    <td >size</td>
	    <td >软件包大小（KB）</td>
	</tr>
    <tr>
	    <td >source</td>
	    <td >来源</td>
	</tr>
</table>  

### 2.2 数据示例
#### 2.2.1 repository仓库数据
```bash
curl -X GET "localhost:9210/repository/_search" \
-H 'Content-Type:application/json' \
-d '{"query":{"match":{"full_name.keyword":"tensorflow/tensorflow"}}}' \
--user elastic:iscas139
```
``` json
{
  "took" : 0,
  "timed_out" : false,
  "_shards" : {
    "total" : 3,
    "successful" : 3,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
      "value" : 1,
      "relation" : "eq"
    },
    "max_score" : 7.823779,
    "hits" : [
      {
        "_index" : "repository",
        "_type" : "_doc",
        "_id" : "587fb9a04a03c2336d82e1cacd822cb2",
        "_score" : 7.823779,
        "_source" : {
          "name" : "tensorflow",
          "full_name" : "tensorflow/tensorflow",
          "description" : "An Open Source Machine Learning Framework for Everyone",
          "contributor_num" : 390,
          "star_num" : 178685,
          "fork_num" : 89106,
          "issue_num" : 38255,
          "watch_num" : 7682,
          "pull_request_num" : 23507,
          "release_num" : 203,
          "url" : "https://github.com/tensorflow/tensorflow",
          "commit_num" : 156079,
          "last_year_commit_num" : 17501,
          "last_30_days_commit_num" : 1274,
          "latest_commit_time" : 1699618547,
          "is_supply" : true,
          "deleted_time" : null,
          "created_at" : 1446859160,
          "language" : "C++",
          "size" : 956091,
          "source" : "github",
          "country" : null,
          "source_id" : 45717250,
          "file_path" : "/mnt/SourcePackage3/git/github/250/tensorflow__tensorflow__587fb9a04a03c2336d82e1cacd822cb2",
          "file_soft_link" : "/mnt/SourcePackage3/repo/github.com/tensorflow/tensorflow.git",
          "insert_time" : 1689320326,
          "update_time" : 1699594868
        }
      }
    ]
  }
}
```

#### 2.2.2 software软件数据
```bash
curl -X GET "localhost:9210/software/_search" \
-H 'Content-Type:application/json' \
-d '{"query":{"match":{"purl": "pkg:hackage/dom-lt@0.2.2.1"}}}' \
--user elastic:iscas139
```
``` json
{
    "took": 1,
    "timed_out": false,
    "_shards": {
        "total": 3,
        "successful": 3,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 1,
            "relation": "eq"
        },
        "max_score": 12.514168,
        "hits": [
            {
                "_index": "software",
                "_type": "_doc",
                "_id": "702dcc9e27ea91ba84f469cb176f47ed",
                "_score": 12.514168,
                "_source": {
                    "source_id": "dom-lt@0.2.2.1",
                    "name": "dom-lt",
                    "purl": "pkg:hackage/dom-lt@0.2.2.1",
                    "alias": "dom-lt",
                    "ver": "0.2.2.1",
                    "is_latest_version": false,
                    "is_binary": false,
                    "language": "Haskell",
                    "label": "algorithms,bsd3,graphs,library",
                    "published_time": 1611834382,
                    "is_open_source": true,
                    "description": "The Lengauer-Tarjan graph dominators algorithm.",
                    "source": "hackage",
                    "insert_time": 1693570177,
                    "update_time": 1700098671,
                    "virtual": false,
                    "download_url": "https://hackage.haskell.org/package/dom-lt-0.2.2.1/dom-lt-0.2.2.1.tar.gz",
                    "file_path": "/mnt/SourcePackage3/hackage/225/50b27491a07df94ef6bb6b5815a460e1/dom-lt-0.2.2.1.tar.gz",
                    "modified_num": 0,
                    "licenseCategory": "Permissive"
                }
            }
        ]
    }
}
```
#### 2.2.3 dataset数据
```bash
curl -X GET "localhost:9210/dataset/_search" \
-H 'Content-Type:application/json' \
-d '{"query":{"match":{"full_name.keyword": "amirveyseh/acronym_identification"}}}' \
--user elastic:iscas139
```
``` json
{
    "took": 1,
    "timed_out": false,
    "_shards": {
        "total": 1,
        "successful": 1,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 1,
            "relation": "eq"
        },
        "max_score": 0.6931471,
        "hits": [
            {
                "_index": "dataset",
                "_type": "_doc",
                "_id": "YW1pcnZleXNlaC9hY3JvbnltX2lkZW50aWZpY2F0aW9uX2h1Z2dpbmdmYWNl",
                "_score": 0.6931471,
                "_source": {
                    "name": "acronym_identification",
                    "alias": "acronym_identification",
                    "label": "format:parquet,library:polars,region:us,language_creators:found,size_categories:10K<n<100K,license:mit,library:datasets,source_datasets:original,library:mlcroissant,modality:text,arxiv:2010.14678,multilinguality:monolingual,language:en,annotations_creators:expert-generated,acronym-identification,library:pandas,task_categories:token-classification",
                    "description": "Dataset Card for Acronym Identification Dataset\n\nDataset Summary\nThis dataset contains the training, validation, and test data for the Shared Task 1: Acronym Identification of the AAAI-21 Workshop on Scientific Document Understanding.\n\nSupported Tasks and Leaderboards\nThe dataset supports an acronym-identification task, where the aim is to predic which tokens in a pre-tokenized sentence correspond to acronyms. The dataset was released for a Shared… See the full description on the dataset page: https://huggingface.co/datasets/amirveyseh/acronym_identification.",
                    "size": 3649,
                    "vendor": "amirveyseh",
                    "source": "huggingface",
                    "full_name": "amirveyseh/acronym_identification",
                    "insert_time": 1739322616,
                    "update_time": 1739426342,
                    "created_at": 1646234962,
                    "last_modified": 1704771597,
                    "downloads": 469,
                    "s3_url": "https://s3.prod.osssc.ac.cn/yuantu/huggingface/datasets/amirveyseh/acronym_identification.git.tar",
                    "likes": 22
                }
            }
        ]
    }
}
```
#### 2.2.4 model数据
```bash
curl -X GET "localhost:9210/model/_search" \
-H 'Content-Type:application/json' \
-d '{"query":{"match":{"full_name.keyword": "albert/albert-base-v2"}}}' \
--user elastic:iscas139
```
``` json
{
    "took": 0,
    "timed_out": false,
    "_shards": {
        "total": 1,
        "successful": 1,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 1,
            "relation": "eq"
        },
        "max_score": 0.2876821,
        "hits": [
            {
                "_index": "model",
                "_type": "_doc",
                "_id": "YWxiZXJ0L2FsYmVydC1iYXNlLXYyX2h1Z2dpbmdmYWNl",
                "_score": 0.2876821,
                "_source": {
                    "name": "albert-base-v2",
                    "alias": "albert-base-v2",
                    "label": "safetensors,region:us,endpoints_compatible,fill-mask,dataset:bookcorpus,autotrain_compatible,tf,en,pytorch,jax,arxiv:1909.11942,license:apache-2.0,transformers,dataset:wikipedia,albert,rust",
                    "size": 260137,
                    "vendor": "albert",
                    "source": "huggingface",
                    "full_name": "albert/albert-base-v2",
                    "insert_time": 1739409050,
                    "update_time": 1739423841,
                    "created_at": 1646234944,
                    "last_modified": 1708311494,
                    "downloads": 4502396,
                    "likes": 117,
                    "s3_url": "https://s3.prod.osssc.ac.cn/yuantu/huggingface/models/albert/albert-base-v2.git.tar"
                }
            }
        ]
    }
}
```





