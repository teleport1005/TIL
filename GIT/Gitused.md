## GIT 명령어 알아보기
 - `git add 폴더 이름`  
 어떠한 특정 폴더 파일을 작업 이력으로 기록하겠다는 준비
 - `git add --all`  
 모든 파일을 추가  
 ***.gitignore 파일을 생성하여 파일 이름 추가시 해당 파일들은 업로드하지 않음***
 - `git commit -m "커밋 메시지"`  
 add된 파일들을 바탕으로 새로운 변경 사항들, 즉 작업 내용을 커밋 메시지로 이유와 함께 기록

`git status`: 현재 업로드 상태 확인 가능  
`git log`: 작업 이력 확인 가능

- `git restore 폴더 이름`  
기록되지 않은(git add하지 않은) 작업 되돌리기
- `git restore --staged 폴더 이름`  
기록한(git add한) 파일 등록 취소
- `git reset commit id`  
add 후 commit한 파일 되돌리기  
-> ***`git log --oneline`에서 `commit id` 확인 가능***
~~되도록 쓰지 않는 편이 좋다~~



