## Basics

MediatR has two kinds of messages it dispatches:

* Request/response messages, dispatched to a single handler
* Notification messages, dispatched to multiple handlers

### Request/response

* #### Request

Interface:

    using MediatR;

    namespace MediatR
    {
        public interface IRequest<out TResponse> : IBaseRequest
        {
        }
    }

Implement Class:

    public class Ping : IRequest<string> { }

* #### Request Handler

Interface:

    namespace MediatR
    {
        public interface IRequestHandler<in TRequest, TResponse> where TRequest : IRequest<TResponse>
        {
            Task<TResponse> Handle(TRequest request, CancellationToken cancellationToken);
        }
    }    

Implement Class:

    public class PingHandler : IRequestHandler<Ping, string> { 

        public Task<string> Handle(Ping request, CancellationToken cancellationToken) 
        {
            return Task.FromResult("Pong");
        }
    }

* #### Finally, send a message through the mediator:

    var response = await mediator.Send(new Ping());
    Debug.WriteLine(response); // "Pong"

[MediatR](https://github.com/jbogard/MediatR/wiki)