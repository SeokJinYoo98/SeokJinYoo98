# 👋 Yoo Seokjin

C#과 Unity로 장기 클라이언트를 만들고, .NET 서버와 공용 Protocol·규칙 Engine을 함께 개발하고 있습니다.<br>
게임 상태와 기능별 책임을 나누고, 테스트부터 패키징·배포까지 연결하는 데 관심이 있습니다.

<h3 align="center">Tech Stack</h3>

<p align="center">
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/csharp/csharp-original.svg" height="40" alt="C#" title="C#" />
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/unity/unity-original.svg" height="40" alt="Unity" title="Unity" />
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/dotnetcore/dotnetcore-original.svg" height="40" alt=".NET" title=".NET" />
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/nuget/nuget-original.svg" height="40" alt="NuGet" title="NuGet" />
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/githubactions/githubactions-original.svg" height="40" alt="GitHub Actions" title="GitHub Actions" />
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/amazonwebservices/amazonwebservices-original-wordmark.svg" height="40" alt="AWS EC2" title="AWS EC2" />
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/ubuntu/ubuntu-original.svg" height="40" alt="Ubuntu" title="Ubuntu" />
</p>

<p align="center">
  UniTask · DOTween · MSTest · PowerShell · UPM<br />
  TCP / async / await · AWS OIDC · SSH / SCP · systemd
</p>

기존 프로젝트에서는 C++·Unreal Engine, OpenGL(King of Tanks), DirectX(Rendering Framework)도 사용했습니다.

## YuJanggi

로컬·AI·온라인 대국을 지원하는 개인 장기 프로젝트입니다. 클라이언트, 서버, 메시지 계약과 게임 규칙을 네 저장소로 분리했습니다.

![서버 로그와 두 Unity 클라이언트를 함께 확인하는 개발 화면](./assets/개발화면.png)

| 프로젝트 | 역할 |
| --- | --- |
| [YuJanggi.Unity](https://github.com/SeokJinYoo98/YuJanggi.Unity) | 화면·입력, 모드별 대국 흐름, AI와 리플레이 |
| [YuJanggi.Server](https://github.com/SeokJinYoo98/YuJanggi.Server) | TCP 연결·세션, 매칭·포진, 게임 메시지 전달과 Room 정리 |
| [YuJanggi.Protocol](https://github.com/SeokJinYoo98/YuJanggi.Protocol) | 공유 메시지 계약, RequestId, JSON 직렬화와 Packet Framing |
| [YuJanggi.Engine](https://github.com/SeokJinYoo98/YuJanggi.Engine) | Unity에 의존하지 않는 장기 규칙·게임 상태 라이브러리 |

### 구현에서 집중한 부분

- **Client 흐름 분리**: Controller는 입력을 전달하고, Flow는 모드별 처리를 선택하며, GameSession은 Engine과 화면을 연결합니다.
- **Response / Event 구분**: 온라인 이동과 최종 종료 결과는 요청의 승인 응답이 아닌 서버 Event를 수신한 뒤 반영합니다.
- **Server 책임 구분**: `Features/Login`, `Lobby`, `Game`에 Handler → Service → Manager → Domain Object의 역할 규칙을 적용합니다. 빈 Base 계층으로 강제하지 않습니다.
- **공유 계약 분리**: Handler·Session 계약과 요청 검증은 Core에, TCP 송수신은 Transport에, 연결 생명주기는 Connection에 둡니다.
- **상태 소유권 구분**: Lobby는 매칭·포진 준비를 담당하고, GameRoom 생성 이후의 상태와 종료·정리는 Game이 담당합니다.

### CI/CD

- **PR 검증**: Protocol / Engine / Server에서 Restore → Build → MSTest를 실행합니다.
- **공용 패키지 배포**: Tag 버전으로 NuGet `.nupkg`와 UPM `.tgz`를 생성합니다. CD는 성공한 Release Run의 NuGet Artifact를 다시 빌드하지 않고 GitHub Packages에 Publish합니다.
- **Server 배포**: Tag에서 Linux x64 Artifact를 생성하고, CD가 SSH / SCP로 EC2에 배포한 뒤 `yujanggi` systemd 서비스를 재시작·확인합니다.

패키지의 프로젝트별 경로·도구 버전·Artifact 이름은 `workflowConfig.json`에서 관리합니다.<br>
NuGet은 Registry로 제공하고, UPM은 Actions Artifact를 다운로드해 Unity에 설치합니다.

EC2 배포에는 GitHub OIDC를 사용합니다. <br>
Runner 공인 IPv4 `/32`에만 SSH를 임시 허용하고, 배포 후 이번 실행에서 생성한 Security Group Rule ID를 제거합니다.

### 검증과 현재 범위

MSTest로 Engine 규칙·상태, Protocol 직렬화·Framing, Server의 Connection / Lobby / Game 흐름을 검증합니다. <br>
로컬 네트워크에서 매칭부터 이동·종료·Room 제거까지 확인했으며, EC2 배포 후 서비스 재시작과 패키지 버전 로그도 확인했습니다.

서버의 Engine 기반 이동·최종 결과 검증, 실제 사용자 인증과 재접속 복구는 아직 구현하지 않았습니다. <br>
배포 실패 시 자동 롤백과 Runner 강제 종료 시 임시 SSH 규칙 정리도 보완할 영역입니다.

상세 구조와 실행 방법은 각 프로젝트의 README에서 확인할 수 있습니다.

## GitHub Activity

![SeokJinYoo98의 GitHub 기여 활동](https://ghchart.rshah.org/SeokJinYoo98)

[기여 활동 보기](https://github.com/SeokJinYoo98?tab=overview) · [전체 저장소 보기](https://github.com/SeokJinYoo98?tab=repositories)
