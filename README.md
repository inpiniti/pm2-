# 사용한 이유
mobius 를 활용한 IoT 플랫폼 구축 과정 중 성능이슈로 인하여,
멀티스레드로 서버를 돌릴필요가 있었습니다.

javascript 는 기본적으로 싱글 스레드라,
pm2 를 통해 멀티스레드로 동작을 시키자고 하였습니다.

사용 가이드에는 따로 config 설정파일로 돌리지는 않았습니다만,

```
// ecosystem.config.js
module.exports = {
  apps : [{
    script    : "app.js", 
    instances : "max", // 실행시킬 프로세스의 갯수(max로 입력할 경우 최대 갯수로 설정한다.)
    exec_mode : "cluster" // cluster 모드로 어플리케이션을 구동시킨다.
  }]
}

pm2 start ecosystem.config.js 
```

위 코드 처럼 설정파일을 지정하고나서, 그 설정파일을 실행시켜도 되는것 같습니다.

# pm2 사용 가이드
1. pm2 백그라우드 cpu 수 만큼 실행
    ```
    pm2 start mobius.js -i max
    ```
    
    max 대신 숫자를 입력해도 됩니다.
    
2. pm2 백그라운드 실행중인 리스트
    ```
    pm2 list
    ```
3. pm2 서버 재시작
    ```
    pm2 restart mobius
    ```
4. pm2 서버 중지
    ```
    pm2 stop mobius
    ```
5. pm2 app name
    ```
    pm2 start app.js -n newName
    ```
    ```
    pm2 restart id --name newName
    ``` 
    app.js 로 실행시키면, 동작중인 프로그램이 잘 구분가지 않아서
    (app 또는 index 로 지정되어 있기 때문)
    찾아보니 변경하는 방법이 있었음

# 기타

가이드 문서이다 보니 따로 소스는 없습니다.
