## file-download-1
> 문제 URL: https://dreamhack.io/wargame/challenges/37  
> `File Download` 취약점이 존재하는 웹 서비스에서 `flag.py`를 다운로드 받으면 플래그를 획득

### app.py
```python
#!/usr/bin/env python3
import os
import shutil

from flask import Flask, request, render_template, redirect
from flag import FLAG

APP = Flask(__name__)

UPLOAD_DIR = 'uploads'

@APP.route('/')
def index():
    files = os.listdir(UPLOAD_DIR)
    return render_template('index.html', files=files)


@APP.route('/upload', methods=['GET', 'POST'])
def upload_memo():
    if request.method == 'POST':
        filename = request.form.get('filename')
        content = request.form.get('content').encode('utf-8')

        if filename.find('..') != -1:
            return render_template('upload_result.html', data='bad characters,,')

        with open(f'{UPLOAD_DIR}/{filename}', 'wb') as f:
            f.write(content)

        return redirect('/')

    return render_template('upload.html')


@APP.route('/read')
def read_memo():
    error = False
    data = b''

    filename = request.args.get('name', '')

    try:
        with open(f'{UPLOAD_DIR}/{filename}', 'rb') as f:
            data = f.read()
    except (IsADirectoryError, FileNotFoundError):
        error = True


    return render_template('read.html',
                           filename=filename,
                           content=data.decode('utf-8'),
                           error=error)


if __name__ == '__main__':
    if os.path.exists(UPLOAD_DIR):
        shutil.rmtree(UPLOAD_DIR)

    os.mkdir(UPLOAD_DIR)

    APP.run(host='0.0.0.0', port=8000)

```

### Solve
1. 파일이 업로드되는 경로는 `UPLOAD_DIR`의 값인 `./uploads` 라는 것을 알 수 있음
2. `app.py` 에서 `from flag import FLAG` 를 통해 `flag.py`를 불러오기 때문에 `./app.py` 와 동일한 디렉토리인 `./flag.py`에 있을 것임
3. 그러므로 `./uploads/../flag.py`를 사용하면 `flag.py`를 가져올 수 있음