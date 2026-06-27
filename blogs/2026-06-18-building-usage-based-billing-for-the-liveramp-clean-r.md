---
title: "Building Usage-Based Billing for The LiveRamp Clean Room with Spark Execution Metrics"
url: "https://liveramp.com/blog/spark-usage-based-billing"
date: "2026-06-18"
author: "John Pawley"
feed_url: "https://liveramp.com/blog/"
---
LiveRamp built a usage-based billing system for its TEE clean rooms by leveraging Spark execution metrics, avoiding additional processing overhead. The solution uses custom Spark plan nodes to preserve business context throughout query execution, enabling accurate attribution across customers and datasets without slowing workloads.
