# Django 09 Authentication System 02

## 회원가입

UserCreationForm()
-
회원 가입 시 사용자 입력 데이터를 받는 built-in ModelForm

- form = CustomUserCreationForm 설정
- 유효성 검사 후 저장, redirect로 초기화면 나타내기

로직 에러
-
회원가입에 사용하는 UserCreationForm이 대체한 커스텀 유저 모델이 아닌 과거 Django의 기본 유저 모델로 인해 작성된 클래스이기 때문

커스텀 유저 모델을 사용하려면 다시 작성해야 하는 Form
-
UserCreationForm    UserChangeForm

두 Form 모두 class Meta: model = user가 작성된 Form이기 때문에 재작성 필요

```
from django.contrib.auth import get_user_model
from django.contrib.auth.forms import UserCreationForm, UserChageForm

class CustomUserCreationForm(UserCreationForm):
    class Meta(UserCreationForm.Meta):
        model = get_user_model()

class CustomUserChageForm(UserChageForm):
    class Meta(UserChangeForm.Meta):
        model = get_user_model()

```

get_user_model()
-
현재 프로젝트에서 활성화된 사용자 모델(active user model)을 반환하는 함수


회원 탈퇴
-


회원정보 수정
-
UserChangeForm()
- 
회원정보 수정 시 사용자 입력 데이터를 받는 built-in ModelForm

UserChangeForm 사용 시 문제점
-
- user 모델의 모든 정보들(fields)까지 모두 출력됨
- 일반 사용자들이 접근해서는 안되는 정보는 출력하지 않도록 해야 함

> CustomUserChangeForm에서 출력 필드를 다시 조정하기

```
class CustomUserChangeForm(UserChagneForm):
    class Meta(UserChangeForm.Meta):
        model = get_user_model()
        fields = ('first_name', 'last_name', 'email',)
```

비밀번호 변경
-
인증된 사용자의 Session 데이터를 Update 하는 과정

PasswordChangeForm()
- 
비밀번호 변경 시 사용자 입력 데이터를 받는 built-in Form

