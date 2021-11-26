# publishing
- `blog`에서 내용수정 및 추가 완료
    - public, themes 디렉토리는 건들지 않기
- 위치는 `blog`에서 아래 명령어 진행하면 된다.

```bash
hugo

cd public
git add .
git commit -m "message"
git push origin master

cd ..
git add .
got commit -m "message"
git push origin master
```