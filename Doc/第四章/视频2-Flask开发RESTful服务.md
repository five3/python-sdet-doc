# Flask 开发 RESTful 服务

## RESTful定义
RESTFUL是一种网络应用程序的设计风格和开发方式，基于HTTP，可以使用XML格式定义或JSON格式定义。

## RESTFUL特点
1. 每一个URI代表1种资源；
1. 客户端使用GET、POST、PUT、DELETE4个表示操作方式的动词对服务端资源进行操作：GET用来获取资源，POST用来新建资源（也可以用于更新资源），PUT用来更新资源，DELETE用来删除资源；
1. 通过操作资源的表现形式来操作资源；
1. 资源的表现形式是XML或者HTML；
1. 客户端与服务端之间的交互在请求之间是无状态的，从客户端到服务端的每个请求都必须包含理解请求所必需的信息。

## Flask RESTful框架
基于`Flask`开发`RESTful`的框架`Flask-RESTful`。官网地址[http://www.pythondoc.com/Flask-RESTful/index.html](http://www.pythondoc.com/Flask-RESTful/index.html)

### 安装
```bash
pip install flask-restful
```

### 简单样例
```python
from flask import Flask
import flask_restful as restful

app = Flask(__name__)
api = restful.Api(app)

class HelloWorld(restful.Resource):
    def get(self):
        return {'hello': 'world'}

api.add_resource(HelloWorld, '/')

if __name__ == '__main__':
    app.run(debug=True)
```

### 完整样例
```python
from flask import Flask
from flask_restful import reqparse, abort, Api, Resource, fields, marshal_with

app = Flask(__name__)
api = Api(app)


TODOS = {
    'todo1': {'task': 'build an API', "name": "xxx"},
    'todo2': {'task': '?????'},
    'todo3': {'task': 'profit!'},
}


def abort_if_todo_doesnt_exist(todo_id):
    if todo_id not in TODOS:
        abort(404, message="Todo {} doesn't exist".format(todo_id))


parser = reqparse.RequestParser()
parser.add_argument('task', type=str, required=True, help="task field")


resource_fields = {
    'name':   fields.String
}


class Todo(Resource):
    @marshal_with(resource_fields)
    def get(self, todo_id):
        abort_if_todo_doesnt_exist(todo_id)
        return TODOS[todo_id]

    def delete(self, todo_id):
        abort_if_todo_doesnt_exist(todo_id)
        del TODOS[todo_id]
        return '', 204

    def put(self, todo_id):
        args = parser.parse_args()
        task = {'task': args['task']}
        TODOS[todo_id] = task
        return task, 201


class TodoList(Resource):
    def get(self):
        return TODOS

    def post(self):
        args = parser.parse_args()
        todo_id = int(max(TODOS.keys()).lstrip('todo')) + 1
        todo_id = 'todo%i' % todo_id
        TODOS[todo_id] = {'task': args['task']}
        return TODOS[todo_id], 201


api.add_resource(TodoList, '/todos')
api.add_resource(Todo, '/todos/<todo_id>')


if __name__ == '__main__':
    app.run(debug=True)
```
