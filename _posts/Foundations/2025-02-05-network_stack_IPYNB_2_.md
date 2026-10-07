---
layout: post
courses: {'csp': {'week': 26}}
toc: True
codemirror: True
title: Network Stack | HTTP and TCP/IP
description: Frontend and/network/stack Backend application applied to networking layers
permalink: /network/stack
---

## Network Stack 
The Networking Stack in a GitHub Pages → AWS EC2 Interaction

When making an HTTP request using JavaScript's fetch method, several layers of the networking stack come into play. This blog applies to CSA (Computer Science "A") and CSP (Computer Science Principles) projects. The content applies to our application(s) setup, with GitHub Pages interacting with a backend Python or Java web application on AWS EC2.

***Tools in Use***
- ***Docker:*** Encapsulates the backend application for consistent deployment across environments.
- ***Nginx:*** Manages TCP/IP traffic, load balancing, and routing to backend containers.
- ***Certbot:*** Secures communication by managing SSL/TLS certificates for HTTPS.
- ***SQL Database:*** Stores and retrieves data for CRUD operations.
- ***JavaScript Fetch and Promise Handling:*** Enables asynchronous HTTP requests from the GitHub Pages frontend to the backend.
- ***Python Flask API (RESTful):*** Provides the backend framework for handling HTTP requests, defining routes, and interacting with the database.
- ***Java Spring API (RESTful):*** Similarly provides backend framework for HTTP requests.



{% capture challenge0 %}
{% raw %}
Networking overview of the OSI model, including sharing key deployment concepts.
{% endraw %}
{% endcapture %}

{% capture code0 %}
{% raw %}
// Import for GameRunner
import GameControl from '@assets/js/GameEnginev1.1/essentials/GameControl.js';
// Level Code
import GameEnvBackground from '@assets/js/GameEnginev1.1/essentials/GameEnvBackground.js';
import Player from '@assets/js/GameEnginev1.1/essentials/Player.js';
import NPC from '@assets/js/GameEnginev1.1/essentials/Npc.js';
import AiNpc from '@assets/js/GameEnginev1.1/essentials/AiNpc.js';

class CustomLevel {
  constructor(gameEnv) {
    const path = gameEnv.path;
    const width = gameEnv.innerWidth;
    const height = gameEnv.innerHeight;
    
    const bgData = {
        name: 'custom_bg',
        src: path + "/images/gamify/comics/network-stack/7-layers-of-osi-model.png",
    };

    const playerData = {
      id: 'Hero',
      src: path + "/images/gamify/chillguy.png",
      SCALE_FACTOR: 5,
      STEP_FACTOR: 1000,
      ANIMATION_RATE: 50,
      INIT_POSITION: { x: 0, y: height * .15 },
      pixels: { height: 512, width: 384 },
      orientation: { rows: 4, columns: 3 },
      down: { row: 0, start: 0, columns: 3 },
      downRight: { row: 1, start: 0, columns: 3, rotate: Math.PI/16 },
      downLeft: { row: 2, start: 0, columns: 3, rotate: -Math.PI/16 },
      right: { row: 1, start: 0, columns: 3 },
      left: { row: 2, start: 0, columns: 3 },
      up: { row: 3, start: 0, columns: 3 },
      upRight: { row: 1, start: 0, columns: 3, rotate: -Math.PI/16 },
      upLeft: { row: 2, start: 0, columns: 3, rotate: Math.PI/16 },
      hitbox: { widthPercentage: 0.45, heightPercentage: 0.2 },
      keypress: { up: 87, left: 65, down: 83, right: 68 }
    };

    const npcData1 = {
      id: 'Application Layer',
      greeting: 'Layer 7: This is where network applications and their protocols operate. It provides services directly to user applications, such as web browsers and email clients.',
      SCALE_FACTOR: 8,
      INIT_POSITION: { x: width * .06, y: height * .46 },
      visible: false,
      hitbox: { widthPercentage: 0, heightPercentage: 0 },
      reaction: function() { if (this.dialogueSystem) { this.showReactionDialogue(); } else { console.log(this.greeting); } },
      interact: function() { if (this.dialogueSystem) { this.showRandomDialogue(); } }
    };

    const npcData2 = {
      id: 'Presentation Layer',
      greeting: 'Layer 6: This layer is responsible for translating data between the application layer and the network format. It handles data encryption, compression, and translation.',
      SCALE_FACTOR: 8,
      visible: false,
      INIT_POSITION: { x: width * .20, y: height * .46 },
      hitbox: { widthPercentage: 0, heightPercentage: 0 },
      reaction: function() { if (this.dialogueSystem) { this.showReactionDialogue(); } else { console.log(this.greeting); } },
      interact: function() { if (this.dialogueSystem) { this.showRandomDialogue(); } }
    };

    const npcData3 = {
      id: 'Session Layer',
      greeting: 'Layer 5: This layer manages sessions between applications. It establishes, maintains, and terminates connections between local and remote applications.',
      SCALE_FACTOR: 8,
      visible: false,
      INIT_POSITION: { x: width * .34, y: height * .46 },
      hitbox: { widthPercentage: 0, heightPercentage: 0 },
      reaction: function() { if (this.dialogueSystem) { this.showReactionDialogue(); } else { console.log(this.greeting); } },
      interact: function() { if (this.dialogueSystem) { this.showRandomDialogue(); } }
    };  

    const npcData4 = {
      id: 'Transport Layer',
      greeting: 'Layer 4: This layer provides reliable data transfer services to the upper layers. It ensures error recovery and flow control.',
      SCALE_FACTOR: 8,
      visible: false,
      INIT_POSITION: { x: width * .48, y: height * .46 },
      hitbox: { widthPercentage: 0, heightPercentage: 0 },
      reaction: function() { if (this.dialogueSystem) { this.showReactionDialogue(); } else { console.log(this.greeting); } },
      interact: function() { if (this.dialogueSystem) { this.showRandomDialogue(); } }
    };

   const npcData5 = {
      id: 'Network Layer',
      greeting: 'Layer 3: This layer is responsible for routing data across the network. It determines the best path for data to travel from source to destination.',
      SCALE_FACTOR: 8,
      visible: false,
      INIT_POSITION: { x: width * .62, y: height * .46 },
      hitbox: { widthPercentage: 0, heightPercentage: 0 },
      reaction: function() { if (this.dialogueSystem) { this.showReactionDialogue(); } else { console.log(this.greeting); } },
      interact: function() { if (this.dialogueSystem) { this.showRandomDialogue(); } }
    };
    
    const npcData6 = {
      id: 'Data Link Layer',
      greeting: 'Layer 2: This layer is responsible for node-to-node data transfer. It handles error detection and correction from the physical layer.',
      SCALE_FACTOR: 8,
      visible: false,
      INIT_POSITION: { x: width * .76, y: height * .46 },
      hitbox: { widthPercentage: 0, heightPercentage: 0 },
      reaction: function() { if (this.dialogueSystem) { this.showReactionDialogue(); } else { console.log(this.greeting); } },
      interact: function() { if (this.dialogueSystem) { this.showRandomDialogue(); } }
    };
    
     const npcData7 = {
      id: 'Physical Layer',
      greeting: 'Layer 1: This layer is responsible for the physical connection between devices. It transmits raw bitstreams over a physical medium.',
      SCALE_FACTOR: 8,
      visible: false,
      INIT_POSITION: { x: width * .90, y: height * .46 },
      hitbox: { widthPercentage: 0, heightPercentage: 0 },
      reaction: function() { if (this.dialogueSystem) { this.showReactionDialogue(); } else { console.log(this.greeting); } },
      interact: function() { if (this.dialogueSystem) { this.showRandomDialogue(); } }
    };

    const network_wizard = path + "/images/gamify/wizard.png";
    const network_wizard_greeting = "Hello! I'm an expert in networking!";
    const npcWizard = {
      id: "Network Wizard",
      greeting: network_wizard_greeting,
      src: network_wizard,
      SCALE_FACTOR: 7,
      ANIMATION_RATE: 10,
      pixels: { height: 185, width: 163 },
      INIT_POSITION: { x: width * 0.47, y: height * 0 },
      orientation: { rows: 1, columns: 1 },
      // LOCK: use ONLY the 4th row (index 3) for every direction/state
      down:      { row: 0, start: 0, columns: 1 },
      hitbox: { widthPercentage: 0.2, heightPercentage: 0.2 },
      // AI-specific properties (required for AiNpc utility)
      expertise: "default",              // Topic area for backend
      chatHistory: [],                   // Conversation memory
      dialogues: [                       // Random greetings
          "Ask me the layers of the OSI model!",
          "Test my knowledge on NGINX conf files.",
          "What takes more bytes in a data packet the string 'ABC' or the number 123?",
          "How can you tell source of a CORS error, NGINX conf or Application code?",
          "Try a Docker question, how do you run multiple sessions?"
      ],
      knowledgeBase: {                   // Context hints for AI
          default: [
              {
                  question: "What is a data packet?",
                  answer: "A data packet is a unit of data transmitted over a network. It contains both the payload (the actual data) and control information, such as source and destination addresses."
              },
              {
                  question: "What is difference between HTTP and HTTPS?",
                  answer: "HTTP (HyperText Transfer Protocol) is used for transmitting web pages over the internet. HTTPS (HTTP Secure) is the secure version of HTTP, using encryption (SSL/TLS) to protect data during transmission."
              },
              {
                  question: "What is an AWS EC2 instance?",
                  answer: "An AWS EC2 (Elastic Compute Cloud) instance is a virtual server in Amazon's cloud. It allows users to run applications on a scalable and secure infrastructure."
              },
              {
                  question: "How do you register a domain on AWS?",
                  answer: "To register a domain on AWS, you can use the Amazon Route 53 service. It allows you to search for available domain names, register them, and manage DNS settings."
              }
          ]
      },
      // Orchestrator: Handle collision/proximity reactions
      reaction: function() {
          if (this.dialogueSystem) {
              this.showReactionDialogue();
          } else {
              console.log(network_wizard_greeting);
          }
      },
      // Orchestrator: Handle player interaction (E key press)
      interact: function() {
          // Delegate to AiNpc utility for full AI conversation interface
          AiNpc.showInteraction(this);
      }
    };

    this.classes = [
      { class: GameEnvBackground, data: bgData },
      { class: Player, data: playerData },
      { class: NPC, data: npcData1 },
      { class: NPC, data: npcData2 },
      { class: NPC, data: npcData3 },
      { class: NPC, data: npcData4 },
      { class: NPC, data: npcData5 },
      { class: NPC, data: npcData6 },
      { class: NPC, data: npcData7 },
      { class: NPC, data: npcWizard },
    ];

  }
}
export const gameLevelClasses = [CustomLevel];
export { GameControl };
{% endraw %}
{% endcapture %}

{% include runners/game.html
   runner_id="network-stack-0"
   challenge=challenge0
   code=code0
   hide_edit="true"
%}


### HTTP/DNS (Application Layer)
The Application Layer is responsible for providing network services directly to end-user applications. It facilitates communication between software applications and the network.

Application Data: The original data being sent.

#### Frontend (GitHub Pages)
The frontend uses fetch to make HTTP(S) requests to the backend. The domain name of the backend hosted on AWS EC2 is resolved to an IP address using DNS (Domain Name System). The HTTP request is formatted, specifying the method (e.g., GET, POST, PUT, DELETE), headers, and optional body (e.g., JSON payloads for CRUD operations).

#### Backend (AWS EC2 with Docker)
The backend application, running inside Docker containers, processes the request. For database operations:
- **Create**: Inserts new records into the SQL database.
- **Read**: Queries data.
- **Update**: Modifies existing records.
- **Delete**: Removes records.

The backend constructs an HTTP response with a status code, headers, and an optional response body (e.g., JSON data).

**Security**: Certbot ensures that HTTPS (secure HTTP) is enabled by managing SSL/TLS certificates, encrypting all communication.

### Presentation Layer

The Presentation Layer (Layer 6) is responsible for data translation, encryption, and compression.  In the more popular TCP/IP model this is folded into Application Layer.

### Session Layer

The Session Layer (Layer 5) is responsible for establishing, managing, and terminating communication "dialogues" between two applications on different devices.   This layer is part of the Application as well in TCP/IP, the description of this would be for something like websockets.

<div class="mermaid">
graph TD
    subgraph Application [Layer 7: Application]
        A1[HTTP/S, DNS]
        A2[Flask API / Spring API]
        A3[JavaScript Fetch]
    end

    subgraph Presentation [Layer 6: Presentation]
        B1[SSL/TLS, Certbot]
    end

    subgraph Session [Layer 5: Session]
        C1[Session Management]
    end

    subgraph Transport [Layer 4: Transport]
        D1[TCP/UDP]
        D2[Nginx Proxy, Load Balancer]
    end

    subgraph Network [Layer 3: Network]
        E1[IP Routing]
        E2[AWS Network, Internet]
    end

    subgraph DataLink [Layer 2: Data Link]
        F1[Ethernet/Wi-Fi]
    end

    subgraph Physical [Layer 1: Physical]
        G1[Cables, Fiber, Wireless]
    end

    %% Connections
    A1 --> B1
    A2 --> B1
    A3 --> B1
    B1 --> C1
    C1 --> D1
    D1 --> E1
    D2 --> D1
    E1 --> F1
    F1 --> G1
</div>

### TCP/UDP (Transport Layer)
The Transport Layer is responsible for providing reliable data transfer services to the upper layers. It ensures that data is delivered accurately and in the correct sequence.

Transport Layer (TCP): Data is segmented into pieces, typically 1460 bytes (if MTU is 1500)

#### Request
HTTP(S) requests are transmitted using TCP (Transmission Control Protocol). Nginx handles incoming TCP traffic, routing it to the appropriate Docker container or application based on the request path. A three-way TCP handshake establishes a reliable connection between the client (browser) and the server.

#### Response
The HTTP response is sent back over the same TCP connection. TCP ensures the response is delivered accurately and in order.

### IP (Network Layer)
The Network Layer is responsible for routing packets across network boundaries. It handles the logical addressing and routing of packets to ensure they reach their destination.

Network Layer (IP): The TCP segment is encapsulated into an IP packet with a 20-byte IP header.

#### Request
TCP segments carrying the HTTP request are encapsulated into IP packets with source and destination IP addresses. The packets are routed through the internet via routers to the AWS EC2 server.

#### Response
The server’s IP address sends IP packets back to the client, carrying the HTTP response data.

**AWS Infrastructure**: AWS handles routing and load balancing as needed within its data center.

## Data Link Layer

Data Link Layer (Frame): The IP packet is placed inside an Ethernet frame, adding MAC addresses and a 4-byte CRC tail.

### Physical Layer
The Physical Layer is responsible for the transmission and reception of raw bit streams over a physical medium. It converts data into electrical, optical, or radio signals, which are representations of binary data (0s and 1s).

[ Physical Layer - Electrical/Optical Signal ]
-----------------------------------------------------------------------------

| Frame |  IP   |  TCP  |  Application Data  |  Frame  |
| Hdr   |  Hdr  |  Hdr  |  (Payload)         |  Tail   |
| (14B) | (20B) | (20B) |  (up to 1460B)     |  (4B)   |
-----------------------------------------------------------------------------

| <--- IP Packet (MTU 1500) ---> |
| <--- Ethernet Frame (1518 bytes total) ---> |


#### Request & Response
IP packets are converted into physical signals appropriate for the medium (e.g., Ethernet, Wi-Fi, or fiber optics). These signals, representing binary data, traverse physical infrastructure, including cables, wireless access points, and routers.

This addition helps to clarify that the physical signals are essentially binary data being transmitted over various media.

## NGINX as Orchestrator

Nginx helps connect all traffic from the internet to and from the backend server.


```python
server {
    # ==============================================================================
    # REVERSE PROXY: DNS to Internal Port Mapping
    # ==============================================================================
    # KEY CONCEPT: This nginx server acts as a REVERSE PROXY
    #
    # THE FLOW:
    # 1. DNS Resolution: flask.opencodingsociety.com → opencodingsociety.com → 3.233.212.71
    # 2. Nginx listens on port 80/443 (standard HTTP/HTTPS ports)
    # 3. Nginx receives the request for flask.opencodingsociety.com
    # 4. Nginx FORWARDS (proxies) the request to localhost:8587 (Flask app)
    # 5. Flask processes the request and returns response to nginx
    # 6. Nginx sends the response back to the client
    #
    # NETWORK LAYERS: How data travels across the internet
    # When browser sends request → travels DOWN the OSI layers:
    #   Layer 7 (Application): HTTP/HTTPS request created
    #   Layer 6 (Presentation): Encryption (TLS/SSL)
    #   Layer 5 (Session): Connection management
    #   Layer 4 (Transport): TCP segments with ports (443)
    #   Layer 3 (Network): IP packets with addresses (24.18.xxx.xxx → 3.233.212.71)
    #   Layer 2 (Data Link): Ethernet frames (MAC addresses)
    #   Layer 1 (Physical): Electrical signals on wire/fiber
    #
    # At server → travels UP the layers:
    #   Physical signals → Ethernet → IP packets → TCP → HTTP → NGINX processes
    #
    # Response follows same path backwards (down on server, up at client)
    #
    # WHY USE A REVERSE PROXY? (Key Teaching Points)
    # - SECURITY: Flask app only listens on localhost (not exposed to internet)
    # - SSL/TLS: Nginx handles HTTPS encryption (certbot/Let's Encrypt integration)
    # - PORT MAPPING: Users access standard port 80/443, not obscure port 8587
    # - MULTIPLE APPS: One server can host many apps on different ports
    #   Example: flask.opencodingsociety.com → localhost:8587, spring.opencodingsociety.com → localhost:8585
    # - LOAD BALANCING: Can distribute requests across multiple backend servers
    # - CACHING: Nginx can cache responses to improve performance
    #
    # WITHOUT REVERSE PROXY: Users would need flask.opencodingsociety.com:8587
    # WITH REVERSE PROXY: Users access clean URL flask.opencodingsociety.com
    # ==============================================================================
    listen 80;
    listen [::]:80;
    server_name flask.opencodingsociety.com;

    # ==============================================================================
    # WEBSOCKET PROXY: Real-Time Bidirectional Communication
    # ==============================================================================
    # Socket.IO enables REAL-TIME features: live chat, notifications, collaborative editing
    # 
    # WEBSOCKET vs HTTP:
    #   HTTP: Request → Response → Connection closes (like a letter)
    #   WebSocket: Persistent connection, bidirectional (like a phone call)
    #
    # UPGRADE HANDSHAKE (How HTTP becomes WebSocket):
    #   1. Browser sends HTTP request with "Upgrade: websocket" header
    #   2. Server responds "101 Switching Protocols"
    #   3. Same TCP connection is now upgraded to WebSocket protocol
    #   4. Both sides can now send messages anytime (no request/response pattern)
    #
    # WHY SEPARATE location /socket.io/ BLOCK?
    #   - Socket.IO connections need special headers: Upgrade, Connection
    #   - Without these headers, WebSocket upgrade fails → falls back to polling (slower)
    #   - This block ensures WebSocket connections are properly proxied
    #
    # TEACHING EXAMPLE: Student joins collaborative coding session
    #   - Initial HTTP request to /socket.io/?transport=websocket
    #   - Nginx proxies with Upgrade headers → Flask Socket.IO server
    #   - Connection upgraded to WebSocket
    #   - Now students see each other's code changes in real-time!
    # ==============================================================================
    location /socket.io/ {
        # Forward Socket.IO traffic to Socket.IO server on port 8500
        proxy_pass http://localhost:8500;
        
        # Use HTTP/1.1 (required for WebSocket support)
        proxy_http_version 1.1;
        
        # CRITICAL: Pass upgrade headers from client to Flask
        # $http_upgrade = client's Upgrade header value (e.g., "websocket")
        proxy_set_header Upgrade $http_upgrade;
        
        # CRITICAL: Tell Flask to upgrade the connection
        # "upgrade" value signals connection should be upgraded
        proxy_set_header Connection "upgrade";
        
        # Preserve original domain for Flask
        proxy_set_header Host $host;
        
        # Preserve student's real IP address
        proxy_set_header X-Real-IP $remote_addr;
    }

    # ==============================================================================
    # PROXY CONFIGURATION: Forwarding to Backend Application
    # ==============================================================================
    # location / means "match ALL paths" (/, /api/users, /api/posts, etc.)
    # Everything (except /socket.io/) goes to the Flask application on port 8587
    # ==============================================================================
    location / {
        # CRITICAL LINE: Forward all requests to Flask on localhost:8587
        # localhost = this same server (internal communication only)
        # 8587 = the port where Flask is listening (configured in app.py or main.py)
        proxy_pass http://localhost:8587;
        
        # Use HTTP/1.1 for better connection reuse and performance
        proxy_http_version 1.1;
        
        # Preserve original domain: flask.opencodingsociety.com
        proxy_set_header Host $host;

        # ==============================================================================
        # THE COMPLETE REQUEST/RESPONSE STORY
        # ==============================================================================
        # SCENARIO: Student at home visits pages.opencodingsociety.com
        #
        # FORWARD PATH (Request):
        #   1. Student's browser (IP: 24.18.xxx.xxx from home ISP)
        #      → Visits pages.opencodingsociety.com (GitHub Pages: 185.199.110.153)
        #      → Downloads HTML/JavaScript to browser
        #
        #   2. JavaScript in browser makes API call:
        #      GET https://flask.opencodingsociety.com/api/users
        #      → Student's home router → ISP network → Internet
        #      → DNS: flask.opencodingsociety.com → opencodingsociety.com → 3.233.212.71
        #      → Arrives at flask.opencodingsociety.com (3.233.212.71)
        #
        #   3. NGINX (3.233.212.71) receives request at port 443:
        #      Request headers from browser:
        #        Host: flask.opencodingsociety.com
        #        Origin: https://pages.opencodingsociety.com
        #        Client IP: 24.18.xxx.xxx
        #
        #   4. NGINX proxies to localhost:8587 (Flask)
        #      WITHOUT proxy_set_header, Flask would see:
        #        Host: localhost:8587              ← WRONG! Lost the domain
        #        IP: 127.0.0.1                     ← WRONG! Shows nginx, not student
        #
        #      WITH proxy_set_header, Flask correctly sees:
        #        Host: flask.opencodingsociety.com      ← Original domain preserved
        #
        # REVERSE PATH (Response):
        #   Flask → NGINX → Internet → ISP → Home Router → Student's Browser
        #   (Same path backwards)
        #
        # WHY THIS MATTERS:
        # - Flask can log the real student IP for security and analytics
        # - Flask knows the original domain for generating correct URLs
        # - Enables proper CORS validation against pages.opencodingsociety.com
        # ==============================================================================

        # ==============================================================================
        # CORS SECURITY: Origin Validation - BLOCKS UNAUTHORIZED REQUESTERS
        # ==============================================================================
        # This configuration implements a whitelist approach to CORS (Cross-Origin Resource Sharing).
        # In DEPLOYMENT, only requests from approved origins can access this API.
        # 
        # REAL EXAMPLE: pages.opencodingsociety.com (GitHub Pages) → flask.opencodingsociety.com (API)
        #   - Different subdomains = different origins = CORS required!
        #   - Without CORS headers, browser BLOCKS the request (security feature)
        #   - With proper CORS setup, browser allows pages to call flask API
        #
        # This prevents unauthorized websites from making requests to your API.
        # ==============================================================================
        
        set $cors_origin "";  # Start with empty string - deny all by default
        
        # Approve all requests from opencodingsociety.com subdomains
        # Examples: pages.opencodingsociety.com, flask.opencodingsociety.com, dev.opencodingsociety.com
        # Pattern breakdown:
        #   ^https://           - Must use HTTPS (for production security)
        #   (.*\.)?             - Optional subdomain (e.g., "pages.", "dev.", or none)
        #   opencodingsociety\.com$ - Must end with opencodingsociety.com
        if ($http_origin ~* "^https://(.*\.)?opencodingsociety\.com$") {
            set $cors_origin $http_origin;
        }
        
        # Approve GitHub Pages deployments from open-coding-society organization
        # Example: https://open-coding-society.github.io
        if ($http_origin = "https://open-coding-society.github.io") {
            set $cors_origin $http_origin;
        }

        # ==============================================================================
        # CORS HEADERS: Tell browser this origin is allowed
        # ==============================================================================
        # These headers are sent with EVERY response (not just OPTIONS)
        # 'always' ensures headers are added even on error responses (4xx, 5xx)
        # ==============================================================================
        
        # Tell browser: yes, this origin can access the response
        # $cors_origin is set above (only if origin was approved)
        add_header "Access-Control-Allow-Origin" "$cors_origin" always;
        
        # Tell browser: yes, include cookies/auth tokens in cross-origin requests
        # Required for maintaining user sessions across pages → flask
        add_header "Access-Control-Allow-Credentials" "true" always;

        # ==============================================================================
        # CROSS-ORIGIN REQUESTS: 2-PART PROCESS
        # ==============================================================================
        # PART 1: PREFLIGHT CHECK (handled here by nginx)
        #   - Browser sends OPTIONS request to check permissions
        #   - Nginx validates origin and responds with CORS headers
        #   - Never reaches Flask application - handled entirely by nginx
        #   - If origin not approved, browser blocks the entire sequence
        #
        # PART 2: ACTUAL REQUEST (handled by Flask application)
        #   - After preflight succeeds, browser sends the real request (GET, POST, etc.)
        #   - Nginx proxies this request to Flask on localhost:8587
        #   - Flask application processes the business logic and returns response
        #   - Flask may also add CORS headers for non-preflight responses
        #
        # WHY PREFLIGHT? Browser sends OPTIONS when request has:
        #   - Custom headers (like Authorization)
        #   - Methods other than GET/POST
        #   - Content-Type other than simple types
        #
        # This separation improves security (nginx blocks bad origins before they reach app)
        # and performance (nginx handles lightweight preflight checks efficiently).
        # ==============================================================================
        
        if ($request_method = OPTIONS) {
            # Tell browser: these HTTP methods are permitted for cross-origin requests
            # GET/POST = read/create data, PUT = update, DELETE = remove, HEAD = metadata
            add_header "Access-Control-Allow-Methods" "GET, POST, PUT, DELETE, OPTIONS, HEAD" always;
            
            # Cache preflight response for 10 minutes (600 seconds)
            # Browser won't send OPTIONS again for same endpoint during this time
            # Reduces overhead - fewer preflight requests = better performance
            add_header "Access-Control-Allow-MaxAge" 600 always;
            
            # Tell browser: these request headers are allowed in actual request
            # Authorization = JWT tokens, API keys
            # Content-Type = JSON, form data
            # Accept = response format preferences
            add_header "Access-Control-Allow-Headers" "Authorization, Origin, X-Origin, X-Requested-With, Content-Type, Accept" always;
            
            # Return 204 No Content - preflight successful (if origin was approved)
            # Browser now knows it's safe to send the actual request
            return 204;
        }
    }
}

```
