FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["AKSKeyron/AKSKeyron.csproj", "AKSKeyron/"]
RUN dotnet restore "AKSKeyron/AKSKeyron.csproj"
COPY . .
WORKDIR "/src/AKSKeyron"
RUN dotnet build "AKSKeyron.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "AKSKeyron.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "AKSKeyron.dll"]