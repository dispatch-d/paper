# paper

## Name

Officially `superlongnamehardtotypeanditscaresusers`, but you can call it `dispatch-d`.

## Setting up an account

```mermaid
sequenceDiagram
    rect rgb(0,255,100)
        Note left of Client: Set up an account
        Client->>Library: Make an account for me
        rect rgb(0,100,255)
            Note right of Server: To official server
            Client->>Server: Phone number, *Public key*
            Server<<->>Client: Enter verification code
            Server->>Library: Public key signed by server
        end
        Client->>Library: Sign me up to x servers,<br>optionally specifying server(s)
        rect rgb(0,100,255)
            Note right of Server: To official server/<br>community-ran/<br>custom
            Library<<->>Server: Can I have y server URLs?
        end
        %% Client->>Library: User name, optional details
        
        %% Server->>Client: Give me a phone number
        loop x times, to different servers
            Library->>Server: Sign me up to this server
            Note left of Server: Sent with the pkey and the sig
            Note over Server: Checks the pkey sig<br>to see if it is correct
            Server->>Library: A URL for the client to see messages,<br>with an access key
            Library->>Client: Saved to the client
        end
        Client->>Library:Username
        rect rgb(0,100,255)
            Note right of Server: To official server
            Library->>Server: (Username, URLs) or link to custom 'DNS'<br>(elaborated in paper)
        end
    end
```

## A custom 'DNS' for users

@thisiscoding1234 dubbs it 'ULS' (Username Lookup System).

```mermaid
sequenceDiagram
    Library->>Server: Username
    Server->>Library: A random URL of the user
    Note left of Library: This URL is then stored<br>on the client for<br>further use
    Note left of Library: In case this URL is lost, <br>another can always be<br>requested from server
    Note right of Server: To prevent abuse, <br>maybe limit lookups<br>of the same user to<br>once per 6 hours?
```

