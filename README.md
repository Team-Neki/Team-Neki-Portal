# Team-Neki-Portal

`portal.suitestudy.com` 서비스 바로가기 포털.

## 구성
- `index.html` — 포털 페이지 (여기만 수정하면 됨)
- `k8s/` — 배포 매니페스트
  - `kustomization.yaml` — `index.html` 을 `configMapGenerator` 로 ConfigMap 화
  - `deployment.yaml` — nginx 로 정적 페이지 서빙
  - `service.yaml`, `ingressroute-https.yaml`, `certificate.yaml`

## 배포 방식
ArgoCD Application(`argocd/apps/portal.yaml`, Team-Neki-GitOps 레포)이 이 레포의 `k8s/`
경로를 watch한다. `index.html` 수정 후 main 에 push하면 ArgoCD 가 자동 sync 하여 배포된다.
이미지 빌드는 없다(스톡 nginx + ConfigMap 마운트).

## 로컬 확인
```sh
kubectl kustomize k8s        # 매니페스트 렌더 확인
open index.html              # 페이지 미리보기
```
