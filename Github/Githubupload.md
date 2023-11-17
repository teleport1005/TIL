# Github에 프로젝트 공유하기
🌱..🌳

## Github에서 생성한 Git Repository를 내 컴퓨터에 다운로드하기  
1. 해당 Repository 주소 복사
2. 폴더를 생성하고 싶은 곳에서 터미널 실행
3. `git clone Repository 주소` 입력  
    -> Cloning 메시지와 함께 생성된 폴더 확인
4. 터미널에서 해당 폴더로 이동하여 업로드 가능

## 내 컴퓨터에서 생성한 프로젝트를 Github에 업로드하기
1. Git Repository 생성 후 주소 복사
2. Github에 업로드하고 싶은 폴더에서 터미널 실행
``` 
git remote add `origin Repository 주소`
git push --set-upstream origin main
```
3. 상기 명령 진행 후 새로고침하여 Github에 정상 업로드 되었는지 확인

### 내 컴퓨터에서 수정한 새로운 이력을 Github에 업로드하기
     1. `git add --all`을 사용하여 수정한 파일 추가
     2. `git commit -m "커밋 메시지"를 사용하여 수정 내역 저장
     3. `git push`로 Github에 업로드

### Github에서 수정한 이력을 컴퓨터로 가져오기  
      Add file, edit 후 Commit Changes로 저장
      `git pull` 실행
      
      
**commit을 Github와 내 컴퓨터에서 진행 후 동시에 업로드하지 않기**


      
