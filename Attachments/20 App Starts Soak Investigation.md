# Summary
Even at 20 starts per minute, 600MB limit per pod, we still hit some issues during a 2 hours smoke
- Wild scaling!
- A single out of memory exception.
![[Pasted image 20250725163950.png]]

# Out of memory investigation
- All of the failed requests line up with the below error logs. This is to do with serving a cached response for VISTAPOS.

## Condensed Logs

**Machine:** aks-linux147-99579104-vmss00000t-aks-au1-perf-common-1

### 2025-07-25 14:10:43.153000

**Logger:** DownloadResponseCachingMiddleware  
**Level:** error  
**Summary:** Error serving cached response for 'POST' /api/X/software/app/VISTAPOS/X.X.X.X/download Exception of type 'System.OutOfMemoryException' was thrown.,System.OutOfMemoryException,System.Array AllocateNewArray(IntPtr, X, GC_ALLOC_FLAGS), at System.GC.AllocateNewArray(IntPtr typeHandle, X length, GC_ALLOC_FLAGS flags)

### 2025-07-25 14:10:43.257000

**Logger:** DownloadResponseCachingMiddleware  
**Level:** error  
**Summary:** Error in response compression cache middleware for 'POST' /api/X/software/app/VISTAPOS/X.X.X.X/download - continuing without caching Headers are read-only, response has already started.,System.InvalidOperationException,Void ThrowHeadersReadOnlyException(), at Microsoft.AspNetCore.Server.Kestrel.Core.Internal.Http.HttpHeaders.ThrowHeadersReadOnlyException()

### 2025-07-25 14:10:43.363000

**Logger:** Microsoft.AspNetCore.Diagnostics.ExceptionHandlerMiddleware  
**Level:** error  
**Summary:** An unhandled exception has occurred while executing the request. Headers are read-only, response has already started.,System.InvalidOperationException,Void ThrowHeadersReadOnlyException(), at Microsoft.AspNetCore.Server.Kestrel.Core.Internal.Http.HttpHeaders.ThrowHeadersReadOnlyException()

### 2025-07-25 14:10:43.367000

**Logger:** Microsoft.AspNetCore.Server.Kestrel  
**Level:** error  
**Summary:** Connection id 'X', Request id 'X:X': An unhandled exception was thrown by the application. Headers are read-only, response has already started.,System.InvalidOperationException,Void ThrowHeadersReadOnlyException(), at Microsoft.AspNetCore.Server.Kestrel.Core.Internal.Http.HttpHeaders.ThrowHeadersReadOnlyException()

### 2025-07-25 14:10:43.557000

**Logger:** vista.services.cloud.software  
**Level:** error  
**Summary:** Out of memory.