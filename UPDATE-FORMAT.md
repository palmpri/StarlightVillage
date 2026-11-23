# 업데이트 형식 v1

고정 주소: `https://github.com/palmpri/StarlightVillage/releases/latest/download/update.json`

JSON 봉투의 `payload`는 UTF-8 JSON의 Base64, `signature`는 payload 원본 바이트에 대한 RSA-SHA256 서명의 Base64입니다. 검증키는 `update-public-key.xml`이며 런처에도 포함됩니다. 서명키는 배포 PC에 암호화하여 보관하고 업로드하지 않습니다.

payload 필드: `schema: 1`, `updater: 1`, `version`, `minecraft`, `loader`, `files`. 각 파일은 `path`, 버전이 고정된 HTTPS `url`, `sha256`, `size`를 가집니다. `installer`는 전체 설치 파일 안내 메타데이터입니다.

변경 가능한 대상은 관리 모드 JAR와 지정된 런처·업데이터·실행/개인 파일 동기화 스크립트·검사기뿐입니다. 삭제 대상은 이전 설치 기록의 관리 모드로 제한합니다. 경로 이탈, 폴더 연결, 중복, 서명 불일치, 파일 크기·해시 불일치, 버전 하향은 거부합니다.

파일을 임시 폴더에 검증한 뒤 별도 업데이터가 런처 종료를 기다리고 백업·복구 기록을 생성합니다. 실패 시 원본을 복원하며 중단 기록이 있으면 다음 런처 실행 때 복구합니다. 개인 설정과 파일은 수정 대상에서 제외합니다.

배포 순서: 로컬 검사 → 서명 목록 생성 → 초안 릴리스에 전체 파일 업로드·해시 확인 → 최신 릴리스로 공개. 공개된 버전의 파일은 덮어쓰지 않고 수정 버전을 새로 배포합니다.
