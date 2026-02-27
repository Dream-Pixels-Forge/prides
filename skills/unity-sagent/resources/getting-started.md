# Unity SAgent - Resources

## Getting Started

### Project Structure

```
Assets/
├── Scripts/
│   ├── Player/
│   ├── Enemies/
│   ├── UI/
│   └── Managers/
├── Prefabs/
├── Materials/
├── Scenes/
├── Sprites/
└── Settings/
```

### Common Commands

| Command | Purpose |
|---------|---------|
| `UnityPackageManager` | Package management |
| `Window > Analysis > Profiler` | Performance profiling |
| `Window > Analysis > Console` | Debug console |
| `Edit > Project Settings` | Project configuration |

## Quick Reference

### MonoBehaviour Lifecycle

```csharp
void Awake()        // Initialize
void Start()        // Before first frame
void Update()       // Every frame
void FixedUpdate()  // Physics update
void LateUpdate()   // After Update
void OnDestroy()    // Cleanup
```

### Common Components

| Component | Purpose |
|-----------|---------|
| `Transform` | Position, rotation, scale |
| `Rigidbody` | Physics simulation |
| `Collider` | Collision detection |
| `MeshRenderer` | Mesh rendering |
| `Material` | Surface appearance |
| `Animator` | Animation control |
| `Camera` | View rendering |

## External Resources
- [Unity Documentation](https://docs.unity3d.com/)
- [Unity Learn](https://learn.unity.com/)
- [Unity Forum](https://forum.unity.com/)
