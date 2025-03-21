## ex-reg-ex
> 문제 URL: https://dreamhack.io/wargame/challenges/834  
> 문제에서 요구하는 형식의 문자열을 입력하여 플래그를 획득하세요. 플래그는 flag.txt 파일과 FLAG 변수에 있습니다.

### Solve
1. 이 정규 표현식은 다음과 같은 형식의 문자열을 매칭함
```regex
dr\w{5,7}e\d+am@[a-z]{3,7}\.\w+
```

### 각 부분의 의미:
1. **`dr`**: 문자열이 `"dr"`로 시작해야 합니다.
2. **`\w{5,7}`**: `\w`는 알파벳 대소문자, 숫자, 밑줄(`_`)을 포함한 단어 문자를 나타냅니다. `{5,7}`은 그 문자가 5에서 7번 반복됨을 의미합니다. 따라서, `"dr"` 뒤에 알파벳, 숫자, 또는 밑줄이 5~7개 나오는 부분입니다.
3. **`e`**: 그 뒤에 `"e"`라는 문자 하나가 나옵니다.
4. **`\d+`**: `\d`는 숫자를 의미하며, `+`는 하나 이상의 숫자가 나와야 함을 뜻합니다. 즉, `"e"` 뒤에 하나 이상의 숫자가 와야 합니다.
5. **`am`**: 그 뒤에는 `"am"`이라는 문자열이 나옵니다.
6. **`@`**: 그 뒤에 `"@"`가 있어야 합니다.
7. **`[a-z]{3,7}`**: `[a-z]`는 소문자 알파벳을 나타내며, `{3,7}`은 소문자 알파벳이 3개에서 7개 사이로 반복된다는 의미입니다. 따라서 `"@"` 뒤에는 소문자 알파벳이 3~7개가 와야 합니다.
8. **`\.`**: `\.`는 실제 마침표(`.`) 문자를 의미합니다. (정규 표현식에서 `.`은 임의의 문자 하나를 의미하므로, 마침표를 나타내려면 `\.`으로 이스케이프해야 합니다.)
9. **`\w+`**: `\w`는 알파벳, 숫자, 밑줄을 의미하며, `+`는 하나 이상의 문자가 와야 함을 뜻합니다. 즉, 마침표 뒤에는 알파벳, 숫자, 또는 밑줄이 하나 이상 나와야 합니다.

### 예시:
이 정규 표현식은 다음과 같은 형식의 문자열과 매칭됩니다:
- `drabcdefe123am@example.com`