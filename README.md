# 우아한 테크 코스 주말 출근 시트 📋

---
이 프로젝트는 우아한 테크 코스의 주말 및 공휴일 출결 관리를 위해 제작됩니다.

## 기능 요구 사항

- 메인
    - [ ] 활성화된 출근일에 대한 데이터를 반환한다.
        - [ ] 가장 빠른 날짜 기준 오름차순 정렬.
        - [ ] 모든 출근일 데이터를 반환하는데 있어 6개의 상태 데이터를 만든다.
            - [ ] 예약 완료 상태 (출근일 이전).
            - [ ] 예약 가능 상태 (출근일 이전).
            - [ ] 예약 불가능 상태 (출근일 이전).
                - 이미 출근일 인원이 꽉 찼을 경우.
                - 출근 예약 마감시간 ~ 출근일 사이인 경우.
            - [ ] 출근 완료 상태 (출근 당일).
            - [ ] 예약을 하지 않은 상태 (출근 당일).
            - [ ] 출근 불가능 상태 (출근 당일).
                - 출석 limit time을 넘겼을 경우.
    - [ ] 날짜별 인원수를 반환한다.
    - [ ] 등록된 모든 출근일을 반환한다.
    
데이터 요청 get
```javascript
{
    active : [
        {
            date : unix_time,
            is_reservable : boolean,    //예약 가능 상태인가?
            is_reservated : boolean,    //예약 했으면 ture, 아니면 false
            is_attended : boolean,  //출근 했으면 true, 아니면 false
            reservationInfo: {
                max : number ,
                current : number
            }
        }, ...
    ],
    finished : [
        {
            date : unix_time,
            reservationInfo: {
                max : number ,
                current : number
            }            
        }, ...
    ]
}

```
    
- 출석
    - [ ] 사용자 인증 정보와 출석 token, 체온 정보를 입력 받으면 출석으로 등록.
        - 예외: 출근 가능 시간보다 빠르거나 늦을 경우 예외.
        - 예외: 모든 데이터는 not null and not empty.

- 출석부
    - [ ] unixTime를 받으면, 행당 날짜에 따른 데이터를 반환한다.
    - [ ] 예약자 명단을 반환한다.
    - [ ] 예약자의 출석 여부를 반환한다.

- Admin
    - 입력
        - [ ] 새로운 출근일을 입력받을 수 있다.
            - [ ] 출근일, 예약 마감 unix time, 출석 limit time (unix time) 을 받는다.