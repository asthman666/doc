# dotnet core httpclient proxy

`dotnet new console -n ClientTest`

    using System;
    using System.Net;
    using System.Net.Http;

    namespace ClientTest
    {
        class Program
        {
            static void Main(string[] args)
            {
                HttpClient client = null;

                if (args.Length > 1 && !string.IsNullOrWhiteSpace(args[1]))
                {
                    var proxyUri = args[1];
                    var proxy = new WebProxy() {
                        Address = new Uri(proxyUri),
                        UseDefaultCredentials = false
                    };

                    var httpClientHandler = new HttpClientHandler() {
                        Proxy = proxy
                    };

                    client = new HttpClient(handler: httpClientHandler, disposeHandler: true);
                } 
                else 
                {
                    client = new HttpClient();
                }

                var response = client.GetAsync(args[0]).Result;

                var responseBody = response.Content.ReadAsStringAsync().Result;
                Console.WriteLine(responseBody);
            }
        }
    }

`dotnew run "http://visitwebsite" "http://proxyhost:port"`