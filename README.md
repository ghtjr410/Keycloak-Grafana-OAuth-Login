# 키클락과 그라파나를 연결하여 OAuth2 로그인 구현

## Grafana에서 OAuth2 로그인을 구현한 이유
1. Grafana를 배포했을 때 이것도 하나의 서비스라고 본다면 로그인이 필요하다고 생각합니다.
2. Grafana만 로그인이 필요하지않고 다른 서비스들도 로그인이 필요하다면 관리자는 N개의 회원정보가 필요하게됩니다.
3. 따라서 Keycloak을 이용하여 통합 로그인을 구현한다면 이러한 불편함이 없어지지않을까? 라는 생각으로 구현하게되었습니다.

## Front -> Keyclak과 Grafna -> Keycloak의 로그인 흐름을 분명히 다르다.
Front(react)는 Keycloak.js라는 라이브러리를 이용하여 Keycloak과 통신하며
kc-action으로 간편하게 로그인이 가능했습니다.

Grafana는 달랐습니다 DockerCompose로 OAuth 로그인이라는 것을 명시, 기본 로그인 폼 비활성화를 해야했고
로그인 시 Keyclaok 페이지로 이동하기위해서 Url설정을 해야했으며
Keycloak 설정에서 Client Login을 체크하도 Credential을 발급해야지
Token을 요청할 수 있는 구조로 굉장히 까다로운 구조였습니다.

그러나 구현을 하게되면 여러 서비스들 여러 OpenSource들을 하나의 로그인창구로 관리할 수 있어 간편했습니다.
