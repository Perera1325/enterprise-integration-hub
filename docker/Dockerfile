# Base image provided by WSO2 for Micro Integrator
FROM wso2/wso2mi:4.2.0

# Define build arguments for environment injection
ARG ENV=dev

# Copy Carbon Applications (CAR) to the deployment folder
# In a real CI pipeline, this is built via Maven and copied here
COPY ./IntegrationProjectCompositeExporter/target/*.car ${WSO2_SERVER_HOME}/repository/deployment/server/carbonapps/

# Copy environment specific deployment.toml configuration
COPY ./configs/${ENV}/deployment.toml ${WSO2_SERVER_HOME}/conf/deployment.toml

# Copy custom libraries if any (e.g., custom mediators, JDBC drivers)
# COPY ./resources/lib/*.jar ${WSO2_SERVER_HOME}/lib/

# Expose required ports
# 8290: HTTP
# 8253: HTTPS
EXPOSE 8290 8253

# Health check using the management API
HEALTHCHECK --interval=30s --timeout=10s --retries=3 \
  CMD curl -f http://localhost:9201/health || exit 1

# Start the WSO2 Micro Integrator
CMD ["sh", "-c", "${WSO2_SERVER_HOME}/bin/micro-integrator.sh"]
