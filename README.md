[README.md](https://github.com/user-attachments/files/33812730/README.md)
# jp_voice

Lantern Engine 계열 빌드에서 블러드본 음성을 **일본어로 바꿔 주는 모드 생성기**입니다.

게임 데이터의 `sound` 폴더에는 언어별 음성 뱅크(`이름_eng.fsb`, `이름_jaj.fsb` ...)가 들어 있습니다.
지역락이 걸린 게임은 자기 지역 언어의 파일만 요청하기 때문에, 이 스크립트는 그 이름들(`_eng`, `_ded`, `_frf` ...)
자리에 `_jaj.fsb`(일본어)의 내용을 연결한 모드 폴더 `mods/JP Voice`를 만듭니다.

- 게임 원본 파일과 엔진은 **건드리지 않습니다.** 모드 폴더만 만들고, 지우면 원래대로 돌아옵니다.
- 지역/시리얼을 바꾸지 않습니다.
- 가능하면 하드링크로 만들기 때문에 추가 용량이 거의 들지 않습니다.

## 준비물

- Windows, Python 3.8 이상 (exe 버전은 Python 불필요)
- 일본어 음성(`_jaj.fsb`)이 들어 있는 본인 게임 덤프
- 모드 폴더를 읽어서 게임 파일 위에 덮어씌워 주는 빌드 (Lantern Engine 등)

## 사용법

`jp_voice.py`(또는 `jp_voice.exe`)를 엔진 폴더(`Lantern Engine.exe`가 있는 곳)에 두고 실행합니다.

```
python jp_voice.py              터미널 메뉴
python jp_voice.py status       현재 상태 확인
python jp_voice.py apply        일본어 음성 모드 만들기
python jp_voice.py revert       모드 삭제 (원복)
python jp_voice.py test         뱅크를 디코딩해서 원본/일본어 비교 재생
```

### 옵션

| 옵션 | 설명 |
| --- | --- |
| `--game 경로` | 게임 폴더 (`eboot.bin`이 있는 폴더). 기본값은 런처 설정 |
| `--mods 경로` | 모드 폴더. 기본값은 런처 설정 또는 엔진 폴더의 `mods` |
| `apply --only 이름조각` | 이름에 해당 글자가 든 뱅크만 적용 |
| `apply --dry-run` | 아무것도 만들지 않고 계획만 확인 |
| `apply --copy` | 하드링크가 안 될 때 복사로 진행 |
| `--yes` | 확인 질문 생략 |

### 적용 순서

1. `python jp_voice.py status`로 일본어 뱅크가 있는지 확인합니다.
2. `python jp_voice.py apply`로 모드를 만듭니다.
3. 런처의 Mods 페이지에서 **JP Voice**가 켜져 있는지 확인하고 게임을 실행합니다.
4. 로그에 `Mods: N game files replaced`가 보이면 적용된 것입니다.

되돌리려면 `python jp_voice.py revert`를 실행하거나 `mods/JP Voice` 폴더를 삭제하세요.

## 참고

- **같은 드라이브 권장**: 모드 폴더가 게임과 다른 드라이브에 있으면 하드링크가 안 되어 복사로 만들어집니다. 용량이 늘고, 엔진에 따라 실행할 때마다 복사할 수 있으니 같은 드라이브에 두는 걸 권장합니다.
- 덤프에 `_jaj.fsb`가 없으면 이 방식이 통하지 않습니다.
- 일본어 파일이 없는 뱅크는 원래 언어로 남습니다.
- `test` 기능은 [vgmstream](https://github.com/vgmstream/vgmstream)을 사용하며, 없으면 내려받을지 물어봅니다.
- 이 저장소에는 게임 파일이 들어 있지 않습니다. 본인이 가진 게임 데이터에서만 사용하세요.

## 다운로드

[Releases](../../releases/latest)에서 받을 수 있습니다.
