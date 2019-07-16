## Security Spring Boot RESTfull Service используя Auth0 JWT 

### Аутентификация
```
curl -X POST -I 'http://localhost:9000/login?username=tom&password=tompassword'
```

На выходе:
```
HTTP/1.1 200 
Authorization: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJ0b20iLCJleHAiOjE1NjQxMjkwNTR9.CpyDPNGdubdKk_H98L5e1nUPbXsgVNMfB3U21HNGeEMjd7i4nTBn3WQNQefvoPxwZwXIinwm1bLRaX27chc0_w
```

### Получить данные по сотрудникам

#### Без токена:
```
curl -X GET 'http://localhost:9000/employees'
```
На выходе Status 403(Forbidden (Запрещено)):
```
{
  "timestamp":"2019-07-16T08:20:39.371+0000",
  "status":403,
  "error":"Forbidden",
  "message":"Access Denied",
  "path":"/employees"
}
```

#### С токеном:
```
curl -X GET \
  -H 'Authorization: eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJ0b20iLCJleHAiOjE1NjQxMjkwNTR9.CpyDPNGdubdKk_H98L5e1nUPbXsgVNMfB3U21HNGeEMjd7i4nTBn3WQNQefvoPxwZwXIinwm1bLRaX27chc0_w' \
  'http://localhost:9000/employees'
```

На выходе Status 200:
```
[
  {
    "empNo":"E02",
    "empName":"Allen",
    "position":"Salesman"
  },
  {
    "empNo":"E01",
    "empName":"Smith",
    "position":"Clerk"
  },
  {
    "empNo":"E03",
    "empName":"Jones",
    "position":"Manager"
  }
]
```