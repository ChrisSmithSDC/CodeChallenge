FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["CodeChallenge/CodeChallenge.csproj", "CodeChallenge/"]
COPY ["CCLibrary/CCLibrary.csproj", "CCLibrary/"]
RUN dotnet restore "CodeChallenge/CodeChallenge.csproj"
COPY . .
WORKDIR "/src/CodeChallenge"
RUN dotnet build "CodeChallenge.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "CodeChallenge.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "CodeChallenge.dll"]