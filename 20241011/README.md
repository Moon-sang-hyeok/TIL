# DB 02 Many to on relationships 01
## Many to one relationships
- 모델 관계
- Many to one relationships
    N : 1 or 1: N
    -
    한 테이블의 0개 이상의 레코드가 다른 테이블의 레코드 한 개와 관련된 관계
    - Comment(N) - Article(1)
    - Comment - Article
    - 0개 이상의 댓글은 1개의 게시글에 작성될 수 있다.

- 댓글 모델 정의
    -
    - ForeignKey()
        -
        - 한 모델이 다른 모델을 참조하는 관계를 설정하는 필드
        - N:1 관계 표현
        - 데이터베이스에서 외래 키로 구현

```
class Comment(models.Model):
    article = models.ForeignKey(Article, on_delete=models.CASCADE)
```

- ForeignKey(to, on_delete)
    -
- to
    - 참조하는 모델 class 이름

- on_delete
    - 외래 키가 참조하는 객체(1)가 사라졌을때, 외래 키를 가진 객체(N)를 어떻게 처리할 지를 정의하는 설정 (데이터 무결성)
    - 'CASCADE' : 참조 된 객체(부모 객체)가 삭제 될 때 이를 참조하는 모든 객체도 삭제되도록 설정

## 댓글 생성 연습
```
python manage.py shell_plus

Article.objects.create(title='title', content='content')

comment = Comment()

comment.content = 'first comment'

comment.save()

=> NOT NULL constraint failed:
    articles_comment.article_id
=> id 값이 저장 시 누락되었기 때문

article = Article.objects.get(pk=1)

comment.article = article

comment.save()

comment.pk
=> 1

comment.content
=> 'first comment'

comment.article
=> <Article: Article object (1)>

comment.article_id
=> 1

comment.article.pk
=> 1

comment.article.content
=> 'content'
```

## 관계 모델 참조

- 역참조
    - 
    - N:1관계에서 1에서 N을 참조하거나 조회하는 것(1->N)
    - 모델 간의 관계에서 관계를 정의한 모델이 아닌, 관계의 대상이 되는 모델에서 연결된 객체들에 접근하는 방식
    - N은 외래 키를 가지고 있어 물리적으로 참조가 가능하지만, 1은 N에 대한 참조 방법이 존재하지 않아 별도의 역참조 키워드가 필요

- 사용 예시
    -
    article.comment_set.all()

- related manager
    - 
    - N:1 혹은 M:N 관계에서 역참조 시에 사용하는 매니저
    - 'objects' 매니저를 통해 QuerySet API를 사용했던 것처럼 related manager를 통해 QuerySet API를 사용할 수 있게 됨

    ```
    python manage.py shell_plus

    article = Article.objects.get(pk=1)

    >>> article.comment_set.all()
    <QuerySet [<Comment: Comment object (1)>, <Comment: Comment object (2)>]>
    ```

    