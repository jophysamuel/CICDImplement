FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["CICDImplement/CICDImplement.csproj", "CICDImplement/"]
RUN dotnet restore "CICDImplement/CICDImplement.csproj"
COPY . .
WORKDIR "/src/CICDImplement"
RUN dotnet build "CICDImplement.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "CICDImplement.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "CICDImplement.dll"]