# Implement Nakama Server Modules Task

## Purpose

Develop custom Nakama server modules for game-specific server logic, real-time match systems, and backend functionality.

## When to Use

- Implementing custom game logic on Nakama server
- Building real-time multiplayer features
- Creating match-making and lobby systems
- Setting up server-side validation and anti-cheat

## Implementation Phases

### Phase 1: Module Planning

**Identify Server Requirements:**

- Core game mechanics needing server validation
- Real-time features (match-making, lobbies)
- Data management (profiles, sessions, leaderboards)
- Security requirements (anti-cheat, rate limiting)

### Phase 2: Core Module Structure

**Basic Module Template:**

```typescript
function InitModule(
  ctx: nkruntime.Context,
  logger: nkruntime.Logger,
  nk: nkruntime.Nakama,
  initializer: nkruntime.Initializer
) {
  // Register RPC functions
  initializer.registerRpc("create_match", rpcCreateMatch);
  initializer.registerRpc("find_match", rpcFindMatch);

  // Register match handler
  initializer.registerMatch("game_match", {
    matchInit,
    matchJoinAttempt,
    matchJoin,
    matchLeave,
    matchLoop,
    matchTerminate,
  });

  // Register hooks
  initializer.registerBeforeAuthenticate(beforeAuthenticate);
  initializer.registerAfterAuthenticate(afterAuthenticate);
}
```

### Phase 3: Match-Making Implementation

**Create Match System:**

```typescript
function rpcCreateMatch(
  context: nkruntime.Context,
  logger: nkruntime.Logger,
  nk: nkruntime.Nakama,
  payload: string
): string {
  const request = JSON.parse(payload);

  const matchId = nk.matchCreate("game_match", {
    maxPlayers: request.maxPlayers || 4,
    gameMode: request.gameMode || "default",
    private: request.private || false,
  });

  return JSON.stringify({ matchId: matchId });
}
```

### Phase 4: Real-time Match Handler

**Match State Management:**

```typescript
function matchInit(
  context: nkruntime.Context,
  logger: nkruntime.Logger,
  nk: nkruntime.Nakama,
  params: { [key: string]: string }
): nkruntime.MatchState {
  return {
    state: {
      players: new Map(),
      gamePhase: "waiting",
      startTime: 0,
    },
    tickRate: 10,
  };
}

function matchLoop(
  context: nkruntime.Context,
  logger: nkruntime.Logger,
  nk: nkruntime.Nakama,
  dispatcher: nkruntime.MatchDispatcher,
  tick: number,
  state: nkruntime.MatchState,
  messages: nkruntime.MatchMessage[]
): nkruntime.MatchState {
  // Process player inputs
  messages.forEach((message) => {
    const data = JSON.parse(message.data);
    processPlayerInput(state.state, message.sender.user_id, data);
  });

  // Update game logic
  updateGameState(state.state, tick);

  // Broadcast updates
  if (tick % 5 === 0) {
    dispatcher.broadcastMessage(1, JSON.stringify(state.state));
  }

  return state;
}
```

### Phase 5: Data Persistence

**Player Profile Management:**

```typescript
function rpcUpdateProfile(
  context: nkruntime.Context,
  logger: nkruntime.Logger,
  nk: nkruntime.Nakama,
  payload: string
): string {
  const request = JSON.parse(payload);
  const userId = context.userId;

  // Read current profile
  const profiles = nk.storageRead([
    {
      collection: "player_profiles",
      key: "profile",
      userId: userId,
    },
  ]);

  const updatedProfile = { ...profiles[0].value, ...request.updates };

  // Write updated profile
  nk.storageWrite([
    {
      collection: "player_profiles",
      key: "profile",
      userId: userId,
      value: updatedProfile,
    },
  ]);

  return JSON.stringify({ success: true });
}
```

### Phase 6: Security Implementation

**Input Validation:**

```typescript
function validatePlayerInput(input: any): boolean {
  if (!input || typeof input !== "object") return false;

  // Validate position bounds
  if (input.position) {
    return input.position.x >= 0 && input.position.x <= 1000 && input.position.y >= 0 && input.position.y <= 1000;
  }

  return true;
}

function detectCheating(player: any, input: any, deltaTime: number): boolean {
  // Speed hacking detection
  if (input.position) {
    const distance = calculateDistance(player.position, input.position);
    const maxDistance = 500 * (deltaTime / 1000);
    return distance > maxDistance * 1.1;
  }

  return false;
}
```

## Quality Validation

### Completeness Checklist

- [ ] RPC functions implemented
- [ ] Match handler functional
- [ ] Data persistence working
- [ ] Security validation active
- [ ] Error handling comprehensive

### Performance Standards

- [ ] RPC responses under 100ms
- [ ] Match loops within tick budget
- [ ] Database queries optimized
- [ ] Memory usage monitored

## Success Criteria

1. **Functional**: All game requirements implemented
2. **Performance**: Meets latency requirements
3. **Security**: Validates inputs and prevents cheating
4. **Reliable**: Handles errors gracefully
5. **Monitored**: Comprehensive logging available
