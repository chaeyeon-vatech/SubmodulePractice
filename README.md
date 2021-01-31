# 📁 SubmodulePractice

## 📝 Initialize Submodule

### <strong> 1. 서브 모듈 등록 <br> </strong>
```git submodule add https://github.com/chaeyeon-vatech/cysub.git```

### <strong> 2. Git Status 확인/ .gitmodules file 확인<br>  </strong>

```$ git status
On branch master
Your branch is up-to-date with 'origin/master'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   .gitmodules
	new file:   cysub``
  
  
  //.gitmodule
[submodule "DbConnector"]
	path = cysub
	url = https://github.com/chaeyeon-vatech/cysub.git

```

### <strong> 3. Git diff —cached --submodule <br>  </strong>

```
//디렉토리를 서브모듈로 취급 => 파일 수정 사항을 직접 수정하지는 않는다.
//통째로 새로운 커밋으로 취급

diff --git a/.gitmodules b/.gitmodules
new file mode 100644
index 0000000..71fc376
--- /dev/null
+++ b/.gitmodules
@@ -0,0 +1,3 @@
+[submodule "cysub"]
+      path = cysub
+      url = https://github.com/chaeyeon-vatech/cysub.git
Submodule DbConnector 0000000...c3f01dc (new submodule)

```

### <strong> 4. cysub의 변경 사항 커밋  </strong>

(1) cysub에서 commit 및 push<br/>
(2) main branch안 cysub directory에서 pull<br/>
(3) main branch commit 및 push

<br><br>

## 📝 다른 브랜치에서 Pull Request

(1) 다른 브랜치에서 Checkout 후 git submodule update <br/>

    i. 서브 모듈의 리모트 저장소에서 데이터를 가져오고
    ii. 서브 모듈을 포함한 프로젝트의 현재 status에서 checkout해야 할 커밋 정보를 가져와서
    iii. 서브 모듈 프로젝트에 대한 checkout을 한다.

(2) 위와 동일한 방법으로 cysub 변경 사항 커밋 <br/>
(3) Master에서 다른 브랜치로 Pull Request/Issue 작성(Test2)<br/>

``` @ 뒤 commit address 변경됨/ 통째로 새로운 커밋으로 취급```


### ❓ Question

(1) Q: 다수의 서브모듈이 있을 시 한 개만 commit/push하고 싶을 때 다른 서브모듈들도 commit 사항에 뜬다.

    A: 다른 서브모듈들과 clone이 되어있지만 변경사항이 반영되지 않았기 때문에 나타나는 현상
    git clone이 변경사항을 반영하지는 않는다. 메인 프로젝트 입장에서 서브모듈은 사실 단지 현재 가리키는 커밋과 변경 여부만 적혀있는 하나의 파일에 불과하기 때문이다.
    그래서 서브모듈 디렉터리에서 2가지 명령어를 추가로 실행해야 서브모듈의 파일을 모두 가져올 수 있다.
    
```
// git 로컬 저장소 초기화
git submodule init
//서브모듈의 원격 저장소에서 파일 가져옴
git submodule update
```

    (Tip) 애초에 clone 할 때 git clone --recurse-submodules https://github.com/chaeyeon-vatech/cysub.git
     2개의 추가 명령어를 실행하지 않아도 한 번에 초기화 가능
     
(2) Q: 다른 개발자가 추가한 사항 반영할 때는?

   A: 
```
git submodule update --remote cysub
```

(3) Q: 수정 사항 공유도 가능한가?

   A: 
   ```
   git push --recurse-submodules=check

   git push --recurse-submodules=on-demand
   ```
