---
layout: post
title: "SocketIO Protocol"
date: 2018-04-01 23:30
categories: Network
permalink: /archivers/socketio_protocol
---
# Socket-IO Protocol
## 기본 형태
{enginio_type}{?socketio_type}{?multiplexing}{?data}

### enginio_type
* 0: open
    * Socket 연결이 되었을 때
* 1: close
    * Socket 연결이 해제 되었을 때
* 2: ping
    * Server Side에 Ping 응답 요청
* 3: pong
    * Server Side Ping에 대한 응답
* 4: message
    * Message 통신
* 5: upgrade
* 6: noop
### socketio_type
주로 enginio_type[4: message]와 함께 사용이 됩니다.
* 0: connect
    * Event 접속
* 1: disconnect
    * Event 접속 해제
* 2: event
    * Event 메시지 송수신
* 3: ack
* 4: error
* 5: binary_event
* 6: binary_ack

### multiplexing
SocketIO 는 Multiplexing을 지원합니다. '/' 문자열로 namespace를 지원을 하며
multiplexing 사용 중에는 data 구분 자가 ',' 문자열로 사용됩니다.

### data
socketio_type[2:event] 일 경우 text 데이터가 전달되고 socketio_type[5:binary_event] 일 경우 binary 데이터가 전달됩니다. 

## Example
* 0{"sid":"0JoWqM92FLCKO7hnAMmn","upgrades":[],"pingInterval":25000,"pingTimeout":60000}
    * enginio_type[0:open] 서버에 접속을 하였고
    * data로 서버 기본 설정 (ping 주기)을 전달 받았습니다.
* 40/chat
    * enginio_type[4:message]
    * socketio_type[0:connect]
    * namespace chat 으로 접속하였습니다.
* 42/chat,["new message", "test"]
    * enginio_type[4:message]
    * socketio_type[2:event]
    * namespace chat 에서 ["new message", "test"] text 메시지를 받았습니다.

# 참고
* https://github.com/socketio/engine.io-protocol
* https://github.com/socketio/socket.io-protocol