# 사용하고자 하는 포트 번호가 사용 중인 경우, 해당 작업 끝내기

- 나의 경우, 8080 포트가 이미 사용중이라 에러가 떴었다. 
- 이런 경우, 사용하고 있는 8080을 닫아줘야한다.

## 해결방법 (Window OS)

- 관리자 권한으로 명령 프롬프트를 연다. (`ctrl` + `r` --> `cmd`)
- `netstat-ano`을 입력하여, 해당 주소 8080을 사용하고 있는 `PID`를 확인한다.
  - 나의 경우 PID가 5988였다.

    ![check port](https://github.com/user-attachments/assets/ae5c80ee-6363-49e7-b19e-5689ae0a726b)

- `taskkill /pid 5988 /f`를 입력한다. (5988 대신 해당 `PID`를 입력)

  ![taskkill](https://github.com/user-attachments/assets/c2f6a121-a59b-454d-881f-7aaa2a2c7498)

- 위와 같이 성공 메시지가 뜨고 종료된다.