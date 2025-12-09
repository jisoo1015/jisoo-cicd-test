# 1. 파이썬이 깔려 있는 기본 이미지 사용
FROM python:3.11-slim

# 2. 컨테이너 안에서 /app 폴더를 작업 폴더로 사용
WORKDIR /app

# 3. 현재 디렉토리의 app.py 파일을 컨테이너 안 /app으로 복사
COPY app.py .

# 4. 컨테이너에서 열어줄 포트 (나중에 Service에서 targetPort로 사용)
EXPOSE 5000

# 5. 컨테이너가 시작되면 "python app.py" 실행
CMD ["python", "app.py"]

