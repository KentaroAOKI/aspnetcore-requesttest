FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 51795
EXPOSE 44343

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["aspnetcorereqtest/aspnetcorereqtest.csproj", "aspnetcorereqtest/"]
RUN dotnet restore "aspnetcorereqtest/aspnetcorereqtest.csproj"
COPY . .
WORKDIR "/src/aspnetcorereqtest"
RUN dotnet build "aspnetcorereqtest.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "aspnetcorereqtest.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "aspnetcorereqtest.dll"]