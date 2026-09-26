# 👋 Yoo Seokjin

### C# / Unity / .NET Developer  
게임 클라이언트에서 시작해 현재는 **서버·네트워크 구조와 백엔드 개발**까지 확장하고 있습니다.

단순히 기능을 추가하기보다  
**책임을 분리하고, 데이터 소유권과 흐름을 명확하게 만드는 구조**에 관심이 많습니다.

---

## 🔧 Tech Stack

### Language
![C#](https://img.shields.io/badge/C%23-512BD4?style=flat-square&logo=csharp&logoColor=white)

### Client
![Unity](https://img.shields.io/badge/Unity-000000?style=flat-square&logo=unity&logoColor=white)

### Backend / Server
![.NET](https://img.shields.io/badge/.NET-512BD4?style=flat-square&logo=dotnet&logoColor=white)
![TCP](https://img.shields.io/badge/TCP-Networking-blue?style=flat-square)

### Database / Infrastructure
![SQL Server](https://img.shields.io/badge/SQL%20Server-CC2927?style=flat-square&logo=microsoftsqlserver&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black)

---

# 🀄 YuJanggi

현재 가장 집중해서 개발하고 있는 **온라인 장기 프로젝트**입니다.

Unity 클라이언트에 게임 규칙을 직접 결합하는 구조에서 시작해  
Core / Protocol / Client / Server 책임을 분리하는 방향으로 지속적으로 리팩토링하고 있습니다.

## Architecture

```text
                YuJanggi

        ┌──────────────────────┐
        │    Unity Client A    │
        └──────────┬───────────┘
                   │
                   │ TCP
                   ▼
        ┌──────────────────────┐
        │   YuJanggi Server    │
        │                      │
        │  Handshake           │
        │  Matching            │
        │  GameRoom            │
        │  InGame Routing      │
        └──────────┬───────────┘
                   │
                   │ TCP
                   ▼
        ┌──────────────────────┐
        │    Unity Client B    │
        └──────────────────────┘
```

---

## Repository Structure

### 🎮 YuJanggi.Unity

Unity 기반 클라이언트입니다.

```text
Core 기반 게임 진행
NetworkConnection
RequestDispatcher
MatchingHandler
InGameHandler
GameSession
InGameFlow
```

로컬 게임과 네트워크 게임의 실행 흐름을 분리하고 있습니다.

---

### 🖥 YuJanggi.Server.V2

.NET 기반 TCP 게임 서버입니다.

현재 서버는 우선 **두 클라이언트 사이의 네트워크 흐름을 완성하는 것**에 집중하고 있습니다.

```text
YuJanggiServer
│
├─ MatchingHandler
│   └─ MatchMakingService
│       └─ GameRoomManager
│
└─ GameHandler
    └─ GameRoomManager
        └─ GameRoom
            ├─ Cho Client
            └─ Han Client
```

현재 구현 범위:

```text
Client Connect
→ Protocol Handshake
→ Matching Request
→ Matching Found
→ Formation Select
→ GameRoom 생성
→ GameReady
→ GameSceneReady
→ GameStart
```

이후 이동 명령 중계와 서버 권위형 게임 구조를 단계적으로 추가할 예정입니다.

---

### ⚙ YuJanggi.Core.V2

Unity에 의존하지 않는 **순수 C# 장기 엔진**입니다.

```text
Board
Rule
Turn
Score
Record
MatchModel
```

클라이언트와 서버가 동일한 게임 규칙을 사용할 수 있도록  
Unity Runtime과 게임 규칙을 분리하는 것을 목표로 합니다.

---

### 📡 YuJanggi.Protocol.V2

클라이언트와 서버가 공유하는 네트워크 Protocol 프로젝트입니다.

```text
ClientMessage
ServerMessage
Request / Response
Server Event
Protocol DTO
```

Core와 Protocol을 분리하여  
네트워크 계약이 게임 엔진 구현에 직접 의존하지 않도록 구성하고 있습니다.

---

# 🌱 Currently Learning

```text
ASP.NET Core
REST API
SQL / MSSQL
TCP Server Architecture
Server-authoritative Game Architecture
Docker
Linux Deployment
```

---

# 💡 Interests

- C# / .NET Server Development
- TCP Network Programming
- Game Server Architecture
- Server Authoritative Design
- Deterministic Turn-based Game Engine
- Client / Server Shared Core
- Backend Architecture
- Maintainable Software Design

---

# 📌 Development Philosophy

> 기능을 빠르게 추가하는 것보다  
> 각 객체가 어떤 책임을 가지고 어떤 데이터를 소유하는지 명확하게 만드는 것을 중요하게 생각합니다.

게임 개발 과정에서 발생한 구조적 문제를 직접 리팩토링하면서  
클라이언트, 서버, Protocol, Core의 책임을 나누는 과정을 학습하고 있습니다.

---

## GitHub Stats

![GitHub Stats](https://github-readme-stats.vercel.app/api?username=SeokJinYoo98&show_icons=true&hide_border=true)

![Top Languages](https://github-readme-stats.vercel.app/api/top-langs/?username=SeokJinYoo98&layout=compact&hide_border=true)

---

## Contact

GitHub  
**@SeokJinYoo98**
