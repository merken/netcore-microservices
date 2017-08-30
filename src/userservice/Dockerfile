FROM microsoft/aspnetcore
ENV ASPNETCORE_URLS=http://+:80
WORKDIR /app
COPY . /app
ENTRYPOINT ["dotnet", "userservice.dll"]