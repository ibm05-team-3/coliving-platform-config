# coliving-platform-config

Spring Cloud Config 저장소. `prod` 프로필로 기동할 때 서비스별로 넣어야 하는 환경 변수입니다. 값이 비어 있으면 기동이 멈춥니다.

## 기본값

생략하면 아래 값을 씁니다.

| 변수 | 기본값 |
|---|---|
| `DB_PORT` | `5432` |
| `REDIS_PORT` | `6379` |
| `RABBITMQ_PORT` | `5672` |
| `EUREKA_URL` | `http://eureka-server:8761/eureka/` |

`DB_NAME`은 서비스마다 다른 데이터베이스 이름입니다.

gRPC 주소 예:

| 대상 | 값 |
|---|---|
| user-service | `dns:///user-service:9082` |
| property-service | `dns:///property-service:9083` |
| document-service | `dns:///document-service:9087` |
| contract-service | `dns:///contract-service:9089` |

`ROOM_GRPC_TARGET`은 property-service `9083`입니다.

`RABBITMQ_HOST`, `RABBITMQ_USERNAME`, `RABBITMQ_PASSWORD`는 `application-prod.yaml`에 있습니다. Cloud Bus를 쓰는 user-service, community-service, property-service만 읽습니다.

api-gateway, config-server, eureka-server는 이 저장소의 prod yaml을 읽지 않습니다. api-gateway 공개키 변수 이름은 `JWT_SECRET`이고, 서비스 yaml에 데모 키가 기본값으로 들어 있습니다.

## user-service

- `DB_HOST`, `DB_NAME`, `DB_USERNAME`, `DB_PASSWORD`
- `REDIS_HOST`, `REDIS_PASSWORD`
- `RABBITMQ_HOST`, `RABBITMQ_USERNAME`, `RABBITMQ_PASSWORD`
- `NAVER_CLIENT_ID`, `NAVER_CLIENT_SECRET`, `NAVER_REDIRECT_URI`
- `GOOGLE_CLIENT_ID`, `GOOGLE_CLIENT_SECRET`, `GOOGLE_REDIRECT_URI`
- `USER_CRYPTO_KEY`, `FRONTEND_URL`
- `JWT_PUBLIC_KEY`, `JWT_PRIVATE_KEY`

## community-service

- `DB_HOST`, `DB_NAME`, `DB_USERNAME`, `DB_PASSWORD`
- `MONGODB_URI`
- `REDIS_HOST`, `REDIS_PASSWORD`
- `KAFKA_BOOTSTRAP_SERVERS`
- `RABBITMQ_HOST`, `RABBITMQ_USERNAME`, `RABBITMQ_PASSWORD`
- `USER_GRPC_TARGET`, `CONTRACT_GRPC_TARGET`, `PROPERTY_GRPC_TARGET`
- `COMMUNITY_CHAT_ALLOWED_ORIGINS`, `COMMUNITY_CRYPTO_KEY`, `GEMINI_API_KEY`

`GEMINI_API_KEY`는 `community-service.yaml`에 있어 dev에서도 필요합니다. PostgreSQL은 pgvector 인스턴스입니다.

## property-service

- `DB_HOST`, `DB_NAME`, `DB_USERNAME`, `DB_PASSWORD`
- `CONTRACT_GRPC_TARGET`
- `RABBITMQ_HOST`, `RABBITMQ_USERNAME`, `RABBITMQ_PASSWORD`

## contract-service

- `DB_HOST`, `DB_NAME`, `DB_USERNAME`, `DB_PASSWORD`
- `REDIS_HOST`
- `KAFKA_BOOTSTRAP_SERVERS`
- `ROOM_GRPC_TARGET`, `DOCUMENT_GRPC_TARGET`, `USER_GRPC_TARGET`
- `FRONTEND_URL`
- `KAKAOPAY_SECRET_KEY`, `KAKAOPAY_CID`
- `PORTONE_STORE_ID`, `PORTONE_API_SECRET`
- `JWT_PUBLIC_KEY`

## document-service

- `DB_HOST`, `DB_NAME`, `DB_USERNAME`, `DB_PASSWORD`

## reservation-service

- `DB_HOST`, `DB_NAME`, `DB_USERNAME`, `DB_PASSWORD`

## dashboard-service

- `PROPERTY_GRPC_TARGET`
- `ELASTICSEARCH_URIS`, `KAFKA_BOOTSTRAP_SERVERS`, `PROMETHEUS_URL`
