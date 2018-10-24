FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

ENV TZ=America/Los_Angeles
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY TesteDatetime.sln ./
COPY TesteDatetime/TesteDatetime.csproj TesteDatetime/
RUN dotnet restore -nowarn:msb3202,nu1503
COPY . .
WORKDIR /src/TesteDatetime
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "TesteDatetime.dll"]
