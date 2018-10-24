FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

#RUN export TZ="/usr/share/zoneinfo/America/Sao_Paulo"
RUN export TZ="/usr/share/zoneinfo/America/Los_Angeles"

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
