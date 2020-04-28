# "Улучшение безопасности сайта через отключение HTTP хедеров"
## План:
1. Что такое HTTP-хедеры
2. Почему некоторые хедеры нужно отключать
3. Рекомендуемые хедеры для отключения:
	- X-Aspnet-Version 
	- X-Powered-By 
	- X-AspNetMvc-Version 
	- Server
4. Механизмы отключения хедеров
5. Итог 

## Инструменты:
1. Visual Studio 2015 Community
2. Fiddler

<br><br><br><br>

## Механизмы отключения:

X-Aspnet-Version:
```
 <system.web>
    <httpRuntime enableVersionHeader="false" />
  </system.web>
```

X-Powered-By:
```
  <system.webServer>
    <httpProtocol>
      <customHeaders>
        <remove name="X-Powered-By" />
      </customHeaders>
    </httpProtocol>
  </system.webServer>
```

X-AspNetMvc-Version 
```
protected void Application_Start(object sender, EventArgs e)
{
	MvcHandler.DisableMvcResponseHeader = true;
}
```

Server:
```
protected void Application_PreSendRequestHeaders()
{
	Response.Headers.Remove("Server");
}
```

