# Whaleal Platform (WAP) FAQ – Performance Issues

**WAP Version**: 4.0  
**Document Type**: Performance FAQ  
**Description**: This document summarizes common MongoDB performance and cluster stability issues in WAP, with recommended solutions for performance optimization and routine monitoring.

---

> **Severity / Impact Scope Definitions**
>
> - **Severity Levels**: Critical, Major, Minor  
> - **Impact Scope**: Single Node, Cluster, Full Platform

---

## Q9: MongoDB Performance Bottlenecks (High CPU / IO)

**Severity**: Major  
**Impact Scope**: Cluster

**Possible Causes:**

- Frequent full table scans
- Poor index design
- Insufficient hardware resources

**Recommended Solutions:**

- Review slow query logs and `explain()` output
- Focus on key metrics:
  - `totalDocsExamined`
  - `totalKeysExamined`
- Prioritize query and index optimization before considering scaling resources

---

## Q10: Cluster Instability – Frequent Fluctuations or Restarts

**Severity**: Critical  
**Impact Scope**: Cluster

**Possible Causes:**

- Improper WiredTiger cache configuration
- Persistent high disk IO load
- OS parameters not tuned according to best practices

**Recommended Solutions:**

- Check WiredTiger cache configuration ratios
- Use `iostat` to monitor disk IO wait times
- Ensure OS parameters such as THP, NUMA, and `ulimit` are configured correctly
