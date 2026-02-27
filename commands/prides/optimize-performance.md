---
description: Analyze and optimize application performance including profiling, bottleneck detection, and regression prevention. Use {{args}} to specify focus area (load, runtime, bundle, memory, all).
---

# Performance Optimization

**Optimization Focus:** {{args}}

## Instructions

Execute comprehensive performance analysis and optimization.

### Optimization Categories

| Category | Focus | Tools |
|----------|-------|-------|
| **Load Performance** | Page load, TTI, LCP | Lighthouse, WebPageTest |
| **Runtime Performance** | Frame rate, interactions | DevTools Profiler |
| **Bundle Optimization** | Bundle size, code splitting | webpack-bundle-analyzer |
| **Memory Optimization** | Memory leaks, heap | Chrome Memory Profiler |
| **All** | Complete optimization | All tools |

### Phase 1: Performance Audit

1. @performance-sagent: Initial audit
   - Run Lighthouse audit
   - Measure Core Web Vitals
   - Identify performance issues
   - Establish baseline metrics

2. **Metrics Collection**
   - First Contentful Paint (FCP)
   - Largest Contentful Paint (LCP)
   - Cumulative Layout Shift (CLS)
   - Time to Interactive (TTI)
   - Total Blocking Time (TBT)

### Phase 2: Deep Analysis

#### Load Performance
- Analyze critical rendering path
- Identify render-blocking resources
- Check image optimization
- Review caching strategies
- Measure network requests

#### Runtime Performance
- Profile JavaScript execution
- Identify long tasks
- Analyze frame drops
- Check event listener performance
- Measure animation performance

#### Bundle Analysis
- Analyze bundle composition
- Identify large dependencies
- Check for duplicate packages
- Review code splitting
- Measure tree-shaking effectiveness

#### Memory Analysis
- Take heap snapshots
- Identify memory leaks
- Check for detached DOM nodes
- Analyze allocation timelines
- Review garbage collection

### Phase 3: Optimization Implementation

1. @performance-sagent: Prioritize optimizations
   - Impact vs. effort matrix
   - Quick wins first
   - Address critical issues

**Load Optimizations:**
- Implement lazy loading
- Optimize images (WebP, AVIF)
- Enable compression (gzip, brotli)
- Configure caching headers
- Use CDN for assets
- Preload critical resources

**Runtime Optimizations:**
- Debounce/throttle events
- Virtualize long lists
- Memoize expensive calculations
- Optimize re-renders
- Use Web Workers for heavy tasks

**Bundle Optimizations:**
- Remove unused dependencies
- Implement code splitting
- Configure tree-shaking
- Use dynamic imports
- Analyze and replace large packages

**Memory Optimizations:**
- Fix memory leaks
- Clean up subscriptions
- Remove event listeners
- Optimize data structures
- Implement pagination

### Phase 4: Validation

1. @performance-sagent: Re-run audits
   - Compare against baseline
   - Verify improvements
   - Check for regressions

### Performance Budget

| Metric | Target | Warning | Critical |
|--------|--------|---------|----------|
| **LCP** | <2.5s | <4.0s | >4.0s |
| **FCP** | <1.8s | <3.0s | >3.0s |
| **CLS** | <0.1 | <0.25 | >0.25 |
| **TTI** | <3.8s | <7.3s | >7.3s |
| **Bundle Size** | <200KB | <500KB | >500KB |

### Documentation

1. @documentation-sagent: Update performance docs

## Output

Provide performance report:
- Baseline metrics
- Optimizations implemented
- Improved metrics
- Performance score
- Remaining issues
- Monitoring recommendations
