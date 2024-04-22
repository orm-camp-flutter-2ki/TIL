![](https://velog.velcdn.com/images/hee462/post/e4bd4106-60c1-43b6-9c4f-61c0ac499deb/image.png)

> git branch 
- 아직 commit 하지 않은 변경사항 임시로 보관

그래서 기능별로 나눠서 작업함
> git branch feature/{기능}


내 브런치에서 push 할때
> git push origin {내 브런치 이름}

팀원이 머지한 후 pull 받을때
> git pull origin dev
> git checkout {내 브런치}
> git merge dev   // 내브런치랑 pull받은 dev 브런치랑 병합

- 상대방이 pull 한 상태 내 브런치에 업데이트 시키기
![](https://velog.velcdn.com/images/hee462/post/82a7816b-8b74-4925-aee8-ef542dc5156b/image.png)


내가 머지한거 pull 할때
> git checkout dev
> git pull origin dev



이렇게 작업하고 main에서 합쳐주는 작업을 따로 한다고 함 
그렇기 때문에 main은 페어코딩할때는 사용하지 말고 각자 기능역할에 맞는 브랜치를 사용하여 기능구현을 하는것이다.








