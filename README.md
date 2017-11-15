

# 4차산업혁명 선도인재 양성 프로젝트 과정

---
## 1. Week 1 Day 8: 

***



##### Do not repeat yourself



post controller

private

제일 많이 반복되는

```ruby
@post = Post.find(params[:id])	
```



#####post method 안에서만

```ruby
private
def find_post
  @post = Post.find(params[:id])
end

이런식으로
def show
  find_post 
end
```



##### before_action

```ruby
before_action :find_post, only: [:show, :edit, :update] #사용할 method만
```

= before_action 선언으로 인해 find_post가 필요없어진다.



## Rails Way & RESTful

+ 프로젝트를 RESTful 하게

== (정해진 규칙을 따라 만드는) CRUD

== (의미가 더 명확하게 만드는) CRUD

== (HTTP Verb를 활용하여 만드는) CRUD



'/post/show/1'

'/post/show/:id'

1번째 게시물을 보여줘



##### http://meetup.toast.com/posts/92 참고

Verb + Object

HTTP Verb + Object

#### 

### REST API 디자인 가이드

1. URI는 정보의 자원을 표현해야 한다.
2. 정보에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE)로 표현한다.

DELETE /members/1



#### <method>

create -> post

show -> get

update -> put

destroy -> delete

 

#### CoC

Conversation over Configuration

설정보다 '규칙'



#### **규칙**

1. Routing은 RESTful하게
2. Resource는 복수형
   + controller 이름은 복수형으로
   + /posts/index
   + rails g controller posts
3. 단 Model은 단수형
   + rails g model post (테이블은 자동으로 복수형)
   + Post.all / Post.find(1) / Post.destroy



rails g controller tweets index new create edit update destroy

=> == :to



#### tweets RESTful하게

/tweets/new method="post"로 변경

to:    ==   => 같은 뜻

'/' == :root



<%= link_to("게시판가기", "/post/index", method: "post")%>  이름 / 링크 갈곳 / 방법



routes.rb

```ruby
resources :tweets
```



### facebook-board



##### Posts controller

index

new

create

show

edit

update

destroy



##### Post model

string, title

string, content



모든 form은 form_tag

모든 링크는<a>는 link_to로



##### ex)

old : /photo/create/1

사진1개, 모든 사진 보는 경로가 같다

GET /photos 모든사진

POST /photos 1개생성



resources :posts

rake :routes



Prefix = new_post

```ruby
<%= link_to "게시믈 쓰기", new_post_path %>	
```

새로운 method 호출

```ruby
<%= link_to "삭제", post_path(@post.id), method: "delete" %>	
```

redirect_to 3개다 같음

```ruby
redirect_to "/posts/#{@post.id}"
redirect_to post_path(@post.id)
redirect_to post_path(@post)

redirect_to '/'
redirect_to :root
redirect_to root_path
```



삭제 시 메세지 창 alert

```ruby
<%= link_to "삭제", post_path(@post.id), method: "delete", data: {confirm: "진짜 지울거니?"} %>