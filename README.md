# Scam With Your Friends 한국어 음성 인식 패치

게임의 마이크 음성 인식 모델을 **Whisper large-v3-turbo Q5_0**으로 교체하는 Windows용 비공식 패치입니다.

한국어 녹음의 일부 구간에서 기존 base·small 모델보다 자연스러운 전사 결과를 확인했습니다. 실제 게임에서의 정확도와 속도는 PC 사양과 입력 음성에 따라 달라집니다.

## 설치 방법

1. **게임을 완전히 종료**합니다.
2. 패치 ZIP 전체를 일반 폴더에 압축 해제합니다. ZIP 안에서 바로 실행하지 마세요.
3. **`Install.cmd`를 더블클릭**합니다.
4. `Game folder`가 표시되면 게임 설치 폴더 경로를 붙여넣고 Enter를 누릅니다.
5. `Install complete`가 표시되면 게임을 실행하고 **통화 언어를 한국어**로 설정합니다.

설치 폴더는 **Steam 라이브러리 → 게임 우클릭 → 관리 → 로컬 파일 보기**에서 찾을 수 있습니다. 열린 탐색기의 주소 표시줄에서 경로를 복사하세요. `Scam With Your Friends.exe`가 들어 있는 폴더를 입력해야 합니다.

기본 설치 경로의 예시입니다. Steam 라이브러리 위치에 따라 다를 수 있습니다.

```text
C:\Program Files (x86)\Steam\steamapps\common\Scam With Your Friends
```

설치 프로그램은 패치 파일의 체크섬을 확인하고, 설치 직전 모델을 자동 백업한 뒤 교체합니다. 이미 같은 모델이 설치돼 있으면 `Turbo is already installed`라고 표시합니다.

## 친구와 함께 사용할 때

각 플레이어가 **자신의 PC에 따로 설치**해야 합니다. 호스트가 설치한다고 친구의 음성 인식 모델까지 바뀌지는 않습니다.

## 원상복구

1. 게임을 완전히 종료합니다.
2. **`Restore.cmd`를 더블클릭**합니다.
3. 설치할 때와 같은 게임 폴더를 입력합니다.
4. `Restore complete`가 표시되면 게임을 다시 실행합니다.

백업은 게임 설치 폴더의 `SWYF-Speech-Patch-Backup`에 저장됩니다. 이 폴더를 보관해야 설치 직전 상태로 복원할 수 있습니다. 설치 전에 다른 모델을 쓰고 있었다면 그 모델로 돌아갑니다.

다른 업데이트가 모델을 변경한 경우에는 덮어쓰기를 방지하기 위해 복원을 중단합니다. 백업이 없으면 Steam의 **설치된 파일 → 게임 파일 무결성 검사**로 공식 모델을 복구할 수 있습니다. 무결성 검사는 다른 수정 파일도 원래대로 돌릴 수 있습니다.

## 변경 사항

| 항목 | 내용 |
| --- | --- |
| 적용 모델 | Whisper large-v3-turbo, GGML Q5_0 |
| 교체 파일 | `Scam With Your Friends_Data/StreamingAssets/Whisper/ggml-base.bin` |
| 모델 파일 크기 | 574,041,195바이트, 약 547MiB |
| 적용 범위 | 해당 다국어 모델을 사용하는 로컬 음성 인식 |
| 자동 백업 | 게임 폴더의 `SWYF-Speech-Patch-Backup` |

게임이 모델을 찾을 수 있도록 **파일명은 `ggml-base.bin`으로 유지**합니다. 따라서 로그에 base라는 경로가 표시돼도 실제 내용은 turbo일 수 있습니다.

Qwen3 TTS는 NPC의 답변을 음성으로 읽는 별도 기능입니다. 이 패치는 TTS, NPC 대화 지침, 저장 데이터를 수정하지 않습니다. 개인 녹화·대화 로그·계정 정보·게임 실행 파일도 포함하지 않습니다.

## 확인한 결과와 한계

- 별도 테스트 폴더에서 Windows PowerShell을 사용한 설치·중복 설치·원본 복원을 검증했습니다.
- 모든 PC 및 게임 버전에서의 호환성과 실제 플레이 중 속도는 검증하지 않았습니다. 게임과 TTS도 GPU를 사용하므로 실행 후 응답 속도를 확인하세요.
- NPC가 말하거나 답변을 기다리는 동안 입력을 중단하는 게임 동작은 그대로입니다.
- Steam 업데이트나 파일 무결성 검사로 공식 모델이 다시 설치될 수 있습니다.

## 문제 해결

| 표시 또는 증상 | 조치 |
| --- | --- |
| `Wrong folder` | 게임 실행 파일이 들어 있는 설치 폴더를 입력하세요. |
| `Close the game` | 게임을 완전히 종료한 뒤 다시 실행하세요. |
| `Access denied` / 액세스 거부 | 설치 또는 복원 CMD 파일을 우클릭해 관리자 권한으로 실행하세요. |
| `checksum mismatch` | ZIP을 다시 받아 전체 압축을 해제하세요. 백업 오류라면 기존 백업을 임의로 덮어쓰지 마세요. |
| 모델이 변경됐다는 오류 | 업데이트 또는 다른 패치로 파일이 달라진 상태입니다. 설치 프로그램은 기존 백업을 덮어쓰지 않습니다. |
| 인식이 너무 느리거나 문제가 생김 | `Restore.cmd`로 설치 직전 모델을 복원하세요. |
| 말해도 반응이 없음 | NPC 대사가 끝난 뒤 말하고, 내 말이 자막으로 표시되는지 확인하세요. |

CMD 파일의 PowerShell 실행 정책 우회는 **해당 실행에만 적용**되며 시스템 실행 정책을 영구 변경하지 않습니다.

## 포함 파일

```text
SWYF-Korean-Speech-Turbo-v1/
├── README.md
├── 사용방법.txt
├── Install.cmd
├── Restore.cmd
├── Patch.ps1
├── LICENSE-Whisper.txt
└── model/
    └── ggml-large-v3-turbo-q5_0.bin
```

## 출처와 라이선스

- [Whisper large-v3-turbo 모델 설명](https://huggingface.co/openai/whisper-large-v3-turbo)
- [whisper.cpp용 GGML Q5_0 모델](https://huggingface.co/ggerganov/whisper.cpp/blob/main/ggml-large-v3-turbo-q5_0.bin)
- 모델 라이선스: **MIT**. 배포 시 함께 제공된 [LICENSE-Whisper.txt](LICENSE-Whisper.txt)를 유지하세요.

모델 파일의 SHA-256입니다. ZIP 자체의 체크섬은 아닙니다.

```text
394221709CD5AD1F40C46E6031CA61BCE88931E6E088C188294C6D5A55FFA7E2
```
