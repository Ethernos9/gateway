# gateway










spring.application.name=api-gateway
server.port=8765

# Eureka config
#eureka.client.service-url.defaultZone=http://ec2-13-233-159-7.ap-south-1.compute.amazonaws.com:8761/eureka/
eureka.client.service-url.defaultZone=http://localhost:8761/eureka/

spring.cloud.gateway.globalcors.corsConfigurations.[/**].allowedOrigins=http://localhost:5173
spring.cloud.gateway.globalcors.corsConfigurations.[/**].allowedMethods=*
spring.cloud.gateway.globalcors.corsConfigurations.[/**].allowedHeaders=*
spring.cloud.gateway.globalcors.corsConfigurations.[/**].allowCredentials=true

# Gateway routes with CircuitBreaker filter and fallback URIs
spring.cloud.gateway.routes[0].id=profile-service-auth
spring.cloud.gateway.routes[0].uri=lb://PROFILE-SERVICE
spring.cloud.gateway.routes[0].predicates[0]=Path=/auth/**,/profile/**,/oauth2/**

spring.cloud.gateway.routes[1].id=product-service
spring.cloud.gateway.routes[1].uri=lb://PRODUCT-SERVICE
spring.cloud.gateway.routes[1].predicates[0]=Path=/products/**,/openProduct/**

spring.cloud.gateway.routes[2].id=cart-service
spring.cloud.gateway.routes[2].uri=lb://CART-SERVICE
spring.cloud.gateway.routes[2].predicates[0]=Path=/cart/**

spring.cloud.gateway.routes[3].id=order-service
spring.cloud.gateway.routes[3].uri=lb://ORDER-SERVICE
spring.cloud.gateway.routes[3].predicates[0]=Path=/order/**

spring.cloud.gateway.routes[4].id=payment-gateway
spring.cloud.gateway.routes[4].uri=lb://PAYMENT-GATEWAY
spring.cloud.gateway.routes[4].predicates[0]=Path=/checkout/**,/api/**

spring.cloud.gateway.routes[5].id=messaging-service
spring.cloud.gateway.routes[5].uri=lb://MESSAGING-SERVICE
spring.cloud.gateway.routes[5].predicates[0]=Path=/message/**

# Global Filters
spring.cloud.gateway.default-filters[0]=AuthenticationFilter

