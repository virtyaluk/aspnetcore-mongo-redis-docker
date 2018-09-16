FROM node:latest AS node
WORKDIR /source
COPY . .
RUN npm i -g bower
RUN bower install --allow-root

FROM microsoft/dotnet:1.1.9-sdk-1.1.10 AS sdk
WORKDIR /source
COPY --from=node /source .
RUN dotnet restore
RUN dotnet publish -o ./publish -c Release

FROM microsoft/dotnet:1.1.9-runtime AS runtime
WORKDIR /app
COPY --from=sdk /source/publish .
EXPOSE 60000
ENTRYPOINT ["dotnet", "ModernDev.AspNetCore.SimpleApp.dll"]