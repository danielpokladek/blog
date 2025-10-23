+++
date = '2025-10-23'
title = 'Example Post 2'
thumbnail = "resources/_gen/background.svg"
+++

## TOC Headers (H2)
### H3
#### H4

## Shortcode Banner Examples:

{{< alert icon="circle-info" >}}
Info alert example.
{{< /alert >}}

<br>

{{< alert cardColor="#e69539ff" iconColor="#57431dff" textColor="#f1faee" >}}
**Warning!** Warning alert example.
{{< /alert >}}

<br>

{{< alert icon="fire" cardColor="#e63946" iconColor="#1d3557" textColor="#f1faee" >}}
**Error!** Error alert example.
{{< /alert >}}

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.

## C# Application Development

Here's a modern C# example with async/await patterns and dependency injection:

```csharp 
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Logging;
using System.Text.Json;

public class GameEngineService
{
    private readonly ILogger<GameEngineService> _logger;
    private readonly HttpClient _httpClient;

    public GameEngineService(ILogger<GameEngineService> logger, HttpClient httpClient)
    {
        _logger = logger;
        _httpClient = httpClient;
    }

    public async Task<GameData> LoadGameDataAsync(string gameId)
    {
        try
        {
            var response = await _httpClient.GetAsync($"/api/games/{gameId}");
            response.EnsureSuccessStatusCode();
            
            var jsonContent = await response.Content.ReadAsStringAsync();
            var gameData = JsonSerializer.Deserialize<GameData>(jsonContent);
            
            _logger.LogInformation("Successfully loaded game data for {GameId}", gameId);
            return gameData;
        }
        catch (Exception ex)
        {
            _logger.LogError(ex, "Failed to load game data for {GameId}", gameId);
            throw;
        }
    }
}
```

Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit.

## TypeScript Interface Design

Modern TypeScript with generics and advanced type features:

```typescript 
interface RenderContext<T extends MaterialType = StandardMaterial> {
  device: GPUDevice;
  commandEncoder: GPUCommandEncoder;
  material: T;
  viewport: Viewport;
}

type MaterialType = 'standard' | 'pbr' | 'unlit' | 'custom';

class Renderer<TMaterial extends MaterialType> {
  private pipeline: GPURenderPipeline;
  private uniformBuffer: GPUBuffer;

  constructor(
    private device: GPUDevice,
    private shaderModule: GPUShaderModule
  ) {
    this.setupPipeline();
  }

  async render<T extends MaterialType>(
    context: RenderContext<T>,
    meshes: Mesh[]
  ): Promise<void> {
    const passEncoder = context.commandEncoder.beginRenderPass({
      colorAttachments: [{
        view: context.viewport.colorTexture.createView(),
        loadOp: 'clear',
        clearValue: { r: 0.1, g: 0.1, b: 0.1, a: 1.0 },
        storeOp: 'store'
      }]
    });

    for (const mesh of meshes) {
      this.renderMesh(passEncoder, mesh, context.material);
    }

    passEncoder.end();
  }
}
```

Ut enim ad minima veniam, quis nostrum exercitationem ullam corporis suscipit laboriosam, nisi ut aliquid ex ea commodi consequatur? Quis autem vel eum iure reprehenderit qui in ea voluptate velit esse quam nihil molestiae consequatur.

## HLSL Vertex and Fragment Shaders

High-Level Shading Language for DirectX graphics programming:

```hlsl 
struct VSInput
{
    float3 position : POSITION;
    float3 normal : NORMAL;
    float2 texcoord : TEXCOORD0;
    float3 tangent : TANGENT;
};

struct PSInput
{
    float4 position : SV_POSITION;
    float3 worldPos : WORLD_POSITION;
    float3 normal : NORMAL;
    float2 texcoord : TEXCOORD0;
    float3 tangent : TANGENT;
    float3 bitangent : BITANGENT;
};

cbuffer ViewProjectionBuffer : register(b0)
{
    float4x4 viewMatrix;
    float4x4 projectionMatrix;
    float3 cameraPosition;
}

cbuffer ModelBuffer : register(b1)
{
    float4x4 modelMatrix;
    float4x4 normalMatrix;
}

PSInput VSMain(VSInput input)
{
    PSInput output;
    
    float4 worldPos = mul(modelMatrix, float4(input.position, 1.0));
    output.worldPos = worldPos.xyz;
    output.position = mul(projectionMatrix, mul(viewMatrix, worldPos));
    
    output.normal = normalize(mul((float3x3)normalMatrix, input.normal));
    output.tangent = normalize(mul((float3x3)modelMatrix, input.tangent));
    output.bitangent = cross(output.normal, output.tangent);
    output.texcoord = input.texcoord;
    
    return output;
}

float4 PSMain(PSInput input) : SV_TARGET
{
    float3 albedo = tex2D(albedoTexture, input.texcoord).rgb;
    float3 normal = normalize(input.normal);
    float3 lightDir = normalize(lightPosition - input.worldPos);
    
    float NdotL = max(dot(normal, lightDir), 0.0);
    float3 diffuse = albedo * lightColor * NdotL;
    
    float3 viewDir = normalize(cameraPosition - input.worldPos);
    float3 halfDir = normalize(lightDir + viewDir);
    float NdotH = max(dot(normal, halfDir), 0.0);
    float3 specular = pow(NdotH, shininess) * specularColor;
    
    return float4(diffuse + specular, 1.0);
}
```

At vero eos et accusamus et iusto odio dignissimos ducimus qui blanditiis praesentium voluptatum deleniti atque corrupti quos dolores et quas molestias excepturi sint occaecati cupiditate non provident.

## GLSL Fragment Shader

OpenGL Shading Language for cross-platform graphics:

```glsl 
#version 450 core

layout(location = 0) in vec3 fragWorldPos;
layout(location = 1) in vec3 fragNormal;
layout(location = 2) in vec2 fragTexCoord;
layout(location = 3) in vec3 fragTangent;

layout(location = 0) out vec4 fragColor;

layout(binding = 0) uniform sampler2D albedoMap;
layout(binding = 1) uniform sampler2D normalMap;
layout(binding = 2) uniform sampler2D roughnessMap;
layout(binding = 3) uniform sampler2D metallicMap;

layout(std140, binding = 0) uniform SceneData {
    mat4 viewMatrix;
    mat4 projMatrix;
    vec3 cameraPos;
    vec3 lightPos;
    vec3 lightColor;
    float lightIntensity;
};

vec3 calculatePBR(vec3 albedo, float metallic, float roughness, vec3 normal, vec3 viewDir, vec3 lightDir) {
    vec3 F0 = mix(vec3(0.04), albedo, metallic);
    vec3 halfwayDir = normalize(lightDir + viewDir);
    
    float NdotL = max(dot(normal, lightDir), 0.0);
    float NdotV = max(dot(normal, viewDir), 0.0);
    float NdotH = max(dot(normal, halfwayDir), 0.0);
    float VdotH = max(dot(viewDir, halfwayDir), 0.0);
    
    // Cook-Torrance BRDF
    float alpha = roughness * roughness;
    float alpha2 = alpha * alpha;
    
    // Normal Distribution Function
    float denom = NdotH * NdotH * (alpha2 - 1.0) + 1.0;
    float D = alpha2 / (3.14159265 * denom * denom);
    
    // Geometry function
    float k = (roughness + 1.0) * (roughness + 1.0) / 8.0;
    float G1L = NdotL / (NdotL * (1.0 - k) + k);
    float G1V = NdotV / (NdotV * (1.0 - k) + k);
    float G = G1L * G1V;
    
    // Fresnel
    vec3 F = F0 + (1.0 - F0) * pow(1.0 - VdotH, 5.0);
    
    vec3 numerator = D * G * F;
    float denominator = 4.0 * NdotV * NdotL + 0.001;
    vec3 specular = numerator / denominator;
    
    vec3 kS = F;
    vec3 kD = vec3(1.0) - kS;
    kD *= 1.0 - metallic;
    
    return (kD * albedo / 3.14159265 + specular) * lightColor * NdotL;
}

void main() {
    vec3 albedo = texture(albedoMap, fragTexCoord).rgb;
    float metallic = texture(metallicMap, fragTexCoord).r;
    float roughness = texture(roughnessMap, fragTexCoord).r;
    
    vec3 normal = normalize(fragNormal);
    vec3 viewDir = normalize(cameraPos - fragWorldPos);
    vec3 lightDir = normalize(lightPos - fragWorldPos);
    
    vec3 color = calculatePBR(albedo, metallic, roughness, normal, viewDir, lightDir);
    
    // Tone mapping and gamma correction
    color = color / (color + vec3(1.0));
    color = pow(color, vec3(1.0/2.2));
    
    fragColor = vec4(color, 1.0);
}
```

Temporibus autem quibusdam et aut officiis debitis aut rerum necessitatibus saepe eveniet ut et voluptates repudiandae sint et molestiae non recusandae.

## Rust Systems Programming

Modern Rust with ownership and async patterns:

```rust 
use tokio::sync::{mpsc, RwLock};
use std::collections::HashMap;
use std::sync::Arc;
use serde::{Deserialize, Serialize};

#[derive(Debug, Serialize, Deserialize, Clone)]
pub struct RenderCommand {
    pub mesh_id: u64,
    pub material_id: u64,
    pub transform: glam::Mat4,
}

pub struct RenderSystem {
    command_queue: Arc<RwLock<Vec<RenderCommand>>>,
    material_cache: Arc<RwLock<HashMap<u64, Material>>>,
    mesh_cache: Arc<RwLock<HashMap<u64, Mesh>>>,
}

impl RenderSystem {
    pub fn new() -> Self {
        Self {
            command_queue: Arc::new(RwLock::new(Vec::new())),
            material_cache: Arc::new(RwLock::new(HashMap::new())),
            mesh_cache: Arc::new(RwLock::new(HashMap::new())),
        }
    }

    pub async fn submit_command(&self, command: RenderCommand) -> Result<(), RenderError> {
        let mut queue = self.command_queue.write().await;
        queue.push(command);
        Ok(())
    }

    pub async fn render_frame(&self) -> Result<(), RenderError> {
        let commands = {
            let mut queue = self.command_queue.write().await;
            std::mem::take(&mut *queue)
        };

        for command in commands {
            self.render_object(&command).await?;
        }

        Ok(())
    }

    async fn render_object(&self, command: &RenderCommand) -> Result<(), RenderError> {
        let mesh_cache = self.mesh_cache.read().await;
        let material_cache = self.material_cache.read().await;

        let mesh = mesh_cache
            .get(&command.mesh_id)
            .ok_or(RenderError::MeshNotFound(command.mesh_id))?;

        let material = material_cache
            .get(&command.material_id)
            .ok_or(RenderError::MaterialNotFound(command.material_id))?;

        // Render logic here
        self.bind_material(material)?;
        self.draw_mesh(mesh, &command.transform)?;

        Ok(())
    }
}
```

Et harum quidem rerum facilis est et expedita distinctio. Nam libero tempore, cum soluta nobis est eligendi optio cumque nihil impedit quo minus id quod maxime placeat facere possimus.

## Go Microservice

Concurrent programming with goroutines and channels:

```go 
package main

import (
    "context"
    "encoding/json"
    "fmt"
    "log"
    "net/http"
    "sync"
    "time"

    "github.com/gorilla/mux"
    "go.uber.org/zap"
)

type GameServer struct {
    logger   *zap.Logger
    players  sync.Map
    rooms    sync.Map
    eventCh  chan GameEvent
}

type GameEvent struct {
    Type     string      `json:"type"`
    PlayerID string      `json:"player_id"`
    RoomID   string      `json:"room_id"`
    Data     interface{} `json:"data"`
}

func NewGameServer(logger *zap.Logger) *GameServer {
    return &GameServer{
        logger:  logger,
        eventCh: make(chan GameEvent, 1000),
    }
}

func (gs *GameServer) Start(ctx context.Context) error {
    // Start event processor
    go gs.processEvents(ctx)
    
    // Start game tick
    go gs.gameTick(ctx)

    r := mux.NewRouter()
    r.HandleFunc("/api/players/{id}/join", gs.handlePlayerJoin).Methods("POST")
    r.HandleFunc("/api/rooms/{id}/state", gs.handleRoomState).Methods("GET")

    server := &http.Server{
        Addr:    ":8080",
        Handler: r,
    }

    gs.logger.Info("Starting game server on :8080")
    return server.ListenAndServe()
}

func (gs *GameServer) processEvents(ctx context.Context) {
    for {
        select {
        case <-ctx.Done():
            return
        case event := <-gs.eventCh:
            gs.handleGameEvent(event)
        }
    }
}

func (gs *GameServer) gameTick(ctx context.Context) {
    ticker := time.NewTicker(16 * time.Millisecond) // 60 FPS
    defer ticker.Stop()

    for {
        select {
        case <-ctx.Done():
            return
        case <-ticker.C:
            gs.updateGameState()
        }
    }
}

func (gs *GameServer) handlePlayerJoin(w http.ResponseWriter, r *http.Request) {
    vars := mux.Vars(r)
    playerID := vars["id"]

    var joinData struct {
        RoomID string `json:"room_id"`
        Name   string `json:"name"`
    }

    if err := json.NewDecoder(r.Body).Decode(&joinData); err != nil {
        http.Error(w, "Invalid JSON", http.StatusBadRequest)
        return
    }

    event := GameEvent{
        Type:     "player_join",
        PlayerID: playerID,
        RoomID:   joinData.RoomID,
        Data:     joinData,
    }

    select {
    case gs.eventCh <- event:
        w.WriteHeader(http.StatusOK)
        json.NewEncoder(w).Encode(map[string]string{"status": "joined"})
    default:
        http.Error(w, "Server busy", http.StatusServiceUnavailable)
    }
}
```

Curabitur pretium tincidunt lacus. Nulla gravida orci a odio. Nullam varius, turpis et commodo pharetra, est eros bibendum elit, nec luctus magna felis sollicitudin mauris. Integer in mauris eu nibh euismod gravida.

## Conclusion

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
