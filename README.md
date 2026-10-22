# tjdgh4564

Claude와 함께 쓰는 노무 업무 저장소입니다.

## 법령 MCP (국가법령정보센터 연동)

[korean-law-mcp](https://github.com/chrisryugj/korean-law-mcp)를 Claude Code에 등록하면 Claude가 작업할 때 법령·판례·해석례 원문을 직접 조회합니다.

### 처음 한 번 설정하기 (Windows)

1. [Node.js](https://nodejs.org) LTS를 설치합니다.
2. [국가법령정보 공동활용](https://open.law.go.kr)에서 Open API 인증키(OC)를 발급받고, 사용하는 컴퓨터의 공인 IP를 등록합니다.
3. PowerShell에서 Claude Code를 설치합니다.
   ```
   irm https://claude.ai/install.ps1 | iex
   ```
   설치 후 `claude`를 찾을 수 없다는 오류가 나면 아래 명령을 실행하고 PowerShell을 다시 엽니다.
   ```
   [Environment]::SetEnvironmentVariable("Path", [Environment]::GetEnvironmentVariable("Path","User") + ";$env:USERPROFILE\.local\bin", "User")
   ```
4. 법령 MCP를 등록합니다. `내키`를 발급받은 인증키로 바꿉니다.
   ```
   claude mcp add korean-law -s user -e LAW_OC=내키 -- cmd /c npx -y korean-law-mcp@4.15.9
   ```
   인증키는 내 컴퓨터(`%USERPROFILE%\.claude.json`)에만 저장되고 이 저장소에는 올라가지 않습니다.

### 확인하기

1. PowerShell에서 `claude`를 실행합니다.
2. `/mcp`를 입력해 `korean-law`가 connected인지 확인합니다.
3. "근로기준법 제56조 알려줘"처럼 물어봅니다.

### 문제가 생기면

- `failed`로 표시될 때: 인증키를 확인합니다. `claude mcp remove korean-law -s user` 후 4단계를 다시 실행합니다.
- 연결은 되는데 조회가 안 될 때: open.law.go.kr에 등록한 IP가 현재 공인 IP와 같은지 확인합니다.
