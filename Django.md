[TOC]

## 未归类的知识点
1. Django Admin 的更改历史记录仅显示通过 Admin 进行的更改。
2. views 和 urls 的匹配原则：顺序执行，剩余匹配
+ 以 polls/1/results 为例
+ 首先在根urls中按顺序进行匹配，发现匹配项polls/，于是转到polls.urls
```python
urlpatterns = [  
    path("polls/", include("polls.urls")),  
    path('admin/', admin.site.urls),  
]
```
+ 依据剩余匹配原则，此时的url为 1/results，与第三项匹配，1被捕获并命名为question_id作为参数，然后调用views.results
```python
urlpatterns = [  
    path("", views.index, name="index"),  
    path("<int:question_id>/", views.detail, name="detail"),  
    path("<int:question_id>/results/", views.results, name="results"),  
    path("<int:question_id>/vote/", views.vote, name="vote"),  
]
```

## shortcuts库的常用方法

 1. render() 函数的第一个参数是请求对象，第二个参数是模板名称，第三个参数是可选的字典。它会返回一个使用给定上下文渲染的给定模板的 HttpResponse 对象。
`return render(request, "polls/detail.html", {"question": question})`
 2. get_object_or_404() 函数以 Django 模型为第一个参数，并将任意数量的关键字参数传递给模型管理器的 get() 函数。如果对象不存在，它将引发 Http404。
`question = get_object_or_404(Question, pk=question_id)`
 3. get_list_or_404()，其工作原理与 get_object_or_404()相同，只是使用了 filter() 而不是 get()。如果列表为空，它将引发 Http404。
`my_objects = get_list_or_404(MyModel, published=True)`
 4. 


## Django template language (DTL)
DTL语法主要包含四种结构

1. 变量
变量用 {{ 和 }} 包起来，它从一个类似字典的上下文中获取值
`My first name is {{ first_name }}. My last name is {{ last_name }}.`
With a context of **{'first_name': 'John', 'last_name': 'Doe'}**, this template renders to:
`My first name is John. My last name is Doe.`

2. 标签
3. 过滤器
4. 注释
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzMzI5MzA1NiwxNzA0NDUzNDM3LC0zND
gyNjkxNDEsLTE5NDA1NzY5OTksNzg4MDY1MjEzLC0yMDEyNzYx
Nzk2XX0=
-->