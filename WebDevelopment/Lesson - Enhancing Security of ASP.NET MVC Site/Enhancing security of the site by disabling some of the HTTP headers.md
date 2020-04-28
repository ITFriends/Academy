# "Enhancing security of the site by disabling some of the HTTP headers"
## Agenda:
1. What are HTTP headers
2. Why some of the HTTP headers should be disabled
3. Headers recommended for disable:
	- X-Aspnet-Version 
	- X-Powered-By 
	- X-AspNetMvc-Version 
	- Server
4. Means for disable
5. Conslusion

## Tools:
1. Visual Studio 2015 Community
2. Fiddler

<br><br><br><br>

## Means for disable:

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

