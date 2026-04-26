# FROM eclipse-temurin:25-jre-alpine
# COPY target/payment-paypal*.jar app.jar
# ENTRYPOINT ["java", "-jar", "/app.jar"]

# Stage 1: Build bằng Maven
FROM maven:3.9-eclipse-temurin-21-alpine AS build
WORKDIR /app
# Copy toàn bộ code vào để build
COPY . .
# Chạy lệnh build, bỏ qua test để nhanh hơn
RUN mvn clean package -DskipTests

# Stage 2: Chạy ứng dụng
FROM eclipse-temurin:21-jre-alpine
WORKDIR /app
# Chỉ copy duy nhất file thực thi từ stage build sang
COPY --from=build /app/target/payment-paypal-*.jar app.jar
# Kiểm tra nếu bốc nhầm file test thì xóa đi (đề phòng)
RUN rm -f *-tests.jar 2>/dev/null || true

ENTRYPOINT ["java", "-jar", "app.jar"]