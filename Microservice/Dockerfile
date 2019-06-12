FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["Microservice/Microservice.csproj", "Microservice/"]
RUN dotnet restore "Microservice/Microservice.csproj"
COPY . .
WORKDIR "/src/Microservice"
RUN dotnet build "Microservice.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Microservice.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Microservice.dll"]