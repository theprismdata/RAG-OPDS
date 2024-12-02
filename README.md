# README #
OPenDocuSea k8s 구동용
## ngnix ingress controller

## opds-preprocess
사용자가 등록한 문서에서 텍스트를 추출하는 서비스입니다.
open-embedding폴더에서 다음의 명령을 실행합니다.
```
kubectl create configmap embedding-setting-config --from-file=set.yaml
kubectl apply -f  opds-embedding-deploy.yml
```
## opds-summary
추출된 text에 gpt를 결합하여 요약을 수행, 데이터베이스에 저장합니다.
```
kubectl create configmap summary-setting-config --from-file=set.yaml
kubectl apply -f  opds-summary-deploy.yml
```

## opds-embedding
추출된 text에 gpt를 결합하여 행렬로 전환하고 pgvector에 저장합니다.
```
kubectl create configmap embedding-setting-config --from-file=set.yaml
kubectl apply -f  opds-embedding-deploy.yml
```

## opds-chatapi
OPDS LLM 챗봇을 서비스함 RestAPI를 제공  
```
kubectl create configmap chatapi-setting-config --from-file=set.yaml
kubectl apply -f  opds-chatapi-deploy.yml
kubectl apply -f  opds-chatapi-svc.yml
```

```commandline
Request 
http://chatapi 서버 ip: POD 내부 포트<9000>/rqa_post

POST 방식
Query { “user_email”: 사용자 EMAIL ID, “question”:”질문” }
```
