# Foreign Key

> 외래 키
>
> 다른 테이블의 행을 식별할 수 있는 키
>
> 외래 키의 값이 부모테이블의 Primary Key일 필요는 없지만 유일한 값이어야 함 (참조 무결성)



### Foreign Key 선언

```python
# articles/modles.py

class Comment(models.Model):
    # 필드명은 참조하는 클래스 이름의 소문자(단수형), comment.article_id 로 접근 가능
    # 부모테이블과 on_delete는 필수 인자
    article = models.ForeignKey(Article, on_delete=models.CASCADE)
    content = models.CharField(max_length=200)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    def __str__(self):
        return self.content
```

#### on delete

> 부모객체가 사라졌을 때 그것을 참조하던 객체를 어떻게 처리할지에 대한 정의

- `CASCADE` : 이를 참조하는 객체도 삭제

- `PROTECT` : 참조당하고 있는 부모객체가 사라지지 않도록 `ProtectedError`발생

- `RESTRICT` : 참조당하고 있는 부모객체가 사라지지 않도록 `RestrictedError` 발생

- `SET_NULL` : 해당 외래키 값을 `NULL`로 변경, `null=True` 인자를 함께 넘겨줘야만 가능

- `SET_DEFAULT` : 해당 외래키 값을 default값으로 변경, `default` 인자를 설정해줘야 가능

- `SET()` :해당 외래키 값을 SET 안에 설정된 함수에 의해 결정

- `DO_NOTHING` : 그냥 둔다. 참조 무결성을 해칠 위험이 있다

  

### 참조와 역참조

- 참조(`comment.article`) : 자식객체(N)에서 부모객체(1)를 참조
- 역참조(`article.comment_set`) : 부모객체(1)에서 자식객체(N)를 참조
  - `comment_set`은 `Article` 클래스에 실제로 존재하는 관계나 필드가 아님

```python
class Comment(models.Model):
    # related_name 옵션으로 comment_set의 호출명을 바꾸어줄 수 있음
    # 변경 후 article.comment_set은 더이상 사용 불가
    article = models.ForeignKey(Article, on_delete=models.CASCADE, related_name='comments')
```



p32