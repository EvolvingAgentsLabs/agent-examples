# System: Execution State Template

## Overview
This template defines the standard structure for execution state management in LLMunix, enabling pausable, resumable, and trackable workflow execution.

## State Document Structure

### Core State Elements
```yaml
execution_state:
  meta:
    execution_id: "unique identifier for this execution"
    scenario: "name of the scenario being executed"
    goal: "high-level objective"
    start_time: "ISO timestamp of execution start"
    last_update: "ISO timestamp of last state update"
    estimated_completion: "predicted completion time"
    
  status:
    current_step: "name/id of current execution step"
    phase: "major phase of execution (planning/execution/completion)"
    progress_percentage: "0-100 percentage completion"
    execution_mode: "EXECUTION or SIMULATION"
    paused: "boolean indicating if execution is paused"
    
  variables:
    # Dynamic variables specific to the scenario
    # These change as execution progresses
    
  context:
    # Accumulated context and knowledge
    # Built up during execution
    
  tool_results:
    # Cached results from tool executions
    # For replay and recovery scenarios
```

## Standard State Templates

### Generic Execution State
```json
{
  "execution_state": {
    "meta": {
      "execution_id": "exec_{{timestamp}}_{{random}}",
      "scenario": "{{scenario_name}}",
      "goal": "{{user_provided_goal}}",
      "start_time": "{{iso_timestamp}}",
      "last_update": "{{iso_timestamp}}",
      "estimated_completion": null,
      "total_steps": null,
      "completed_steps": 0
    },
    "status": {
      "current_step": "initialization",
      "phase": "planning",
      "progress_percentage": 0,
      "execution_mode": "EXECUTION",
      "paused": false,
      "resumable": true,
      "error_state": false
    },
    "variables": {},
    "context": {
      "accumulated_knowledge": [],
      "discovered_insights": [],
      "user_inputs": [],
      "external_data": []
    },
    "tool_results": {},
    "step_history": [],
    "performance_metrics": {
      "total_cost": 0,
      "total_time": 0,
      "tools_used": [],
      "error_count": 0
    }
  }
}
```

### Research Workflow State
```json
{
  "execution_state": {
    "meta": {
      "execution_id": "research_001",
      "scenario": "MarketResearchAnalysis",
      "goal": "Analyze competitive landscape for AI tools market",
      "start_time": "2024-01-15T10:00:00Z",
      "last_update": "2024-01-15T10:30:00Z",
      "estimated_completion": "2024-01-15T12:00:00Z"
    },
    "status": {
      "current_step": "competitor_analysis",
      "phase": "data_collection",
      "progress_percentage": 35,
      "execution_mode": "EXECUTION",
      "paused": false
    },
    "variables": {
      "research_topics": ["AI tools", "market size", "key players"],
      "competitors_identified": ["OpenAI", "Anthropic", "Google"],
      "data_sources": ["company websites", "industry reports", "news articles"],
      "current_competitor": "Anthropic",
      "analysis_depth": "comprehensive"
    },
    "context": {
      "market_overview": "AI tools market showing 40% YoY growth...",
      "key_trends": ["LLM adoption", "API-first approach", "enterprise focus"],
      "competitive_insights": [
        {
          "company": "OpenAI",
          "strengths": ["first mover", "strong API"],
          "weaknesses": ["reliability issues", "cost"]
        }
      ]
    },
    "tool_results": {
      "web_fetch_001": {
        "url": "https://openai.com",
        "content": "cached website content...",
        "timestamp": "2024-01-15T10:15:00Z"
      },
      "summarization_001": {
        "input": "openai_content",
        "summary": "OpenAI offers API access to GPT models...",
        "confidence": 0.92
      }
    }
  }
}
```

### Multi-Agent Workflow State
```json
{
  "execution_state": {
    "meta": {
      "execution_id": "multiagent_001",
      "scenario": "ContentCreationPipeline",
      "goal": "Create comprehensive blog post about AI trends",
      "start_time": "2024-01-15T09:00:00Z",
      "last_update": "2024-01-15T10:45:00Z"
    },
    "status": {
      "current_step": "content_writing",
      "phase": "content_creation",
      "progress_percentage": 60,
      "execution_mode": "EXECUTION",
      "paused": false
    },
    "variables": {
      "topic": "AI trends 2024",
      "target_length": 2000,
      "target_audience": "tech professionals",
      "content_style": "informative",
      "seo_keywords": ["AI trends", "machine learning", "automation"]
    },
    "context": {
      "research_complete": true,
      "outline_approved": true,
      "draft_sections": {
        "introduction": "completed",
        "main_trends": "in_progress", 
        "implications": "pending",
        "conclusion": "pending"
      }
    },
    "agent_coordination": {
      "research_agent": {
        "status": "completed",
        "outputs": ["trend_analysis.md", "source_citations.json"]
      },
      "writing_agent": {
        "status": "active",
        "current_section": "main_trends",
        "word_count": 1200
      },
      "seo_agent": {
        "status": "waiting",
        "dependencies": ["complete_draft"]
      }
    },
    "tool_results": {
      "research_web_fetch": {
        "sources": 15,
        "trends_identified": 8,
        "data_quality": "high"
      }
    }
  }
}
```

## State Transition Patterns

### Linear Workflow
```yaml
state_transitions:
  initialization → planning → execution → validation → completion
  
step_progression:
  - step_name: "initialization"
    next_step: "planning"
    completion_criteria: "variables initialized"
    
  - step_name: "planning"
    next_step: "execution"
    completion_criteria: "execution plan created"
    
  - step_name: "execution"
    next_step: "validation"
    completion_criteria: "primary tasks completed"
    
  - step_name: "validation"
    next_step: "completion"
    completion_criteria: "results validated"
    
  - step_name: "completion"
    next_step: null
    completion_criteria: "all outputs generated"
```

### Branching Workflow
```yaml
conditional_transitions:
  - from_step: "analysis"
    conditions:
      - if: "data_sufficient"
        next_step: "reporting"
      - if: "data_insufficient"
        next_step: "additional_research"
      - if: "error_detected"
        next_step: "error_recovery"
        
  - from_step: "additional_research"
    next_step: "analysis"
    completion_criteria: "additional data collected"
```

### Parallel Workflow
```yaml
parallel_execution:
  - parallel_group: "data_collection"
    steps: ["web_research", "document_analysis", "expert_interviews"]
    synchronization_point: "data_synthesis"
    
  - parallel_group: "content_creation"
    steps: ["writing", "visual_design", "seo_optimization"]
    synchronization_point: "content_review"
```

## Error Handling & Recovery

### Error State Structure
```json
{
  "error_state": {
    "has_errors": true,
    "current_error": {
      "error_id": "err_001",
      "step": "web_fetching", 
      "error_type": "network_timeout",
      "error_message": "Connection timeout after 30 seconds",
      "timestamp": "2024-01-15T10:30:00Z",
      "retry_count": 2,
      "max_retries": 3
    },
    "error_history": [
      {
        "error_id": "err_001",
        "resolved": false,
        "resolution_strategy": "retry_with_timeout"
      }
    ],
    "recovery_options": [
      "retry_operation",
      "skip_step",
      "use_cached_data",
      "request_human_intervention"
    ]
  }
}
```

### Recovery Strategies
```yaml
automatic_recovery:
  network_errors: "retry with exponential backoff"
  rate_limiting: "pause and retry after delay"
  transient_failures: "retry up to 3 times"
  
manual_recovery:
  data_quality_issues: "request human review"
  complex_errors: "escalate to human operator"
  business_logic_conflicts: "pause for decision"
  
graceful_degradation:
  partial_failures: "continue with available data"
  optional_steps: "skip non-critical operations"
  fallback_methods: "use alternative approaches"
```

## Performance Tracking

### Metrics Collection
```json
{
  "performance_metrics": {
    "execution_time": {
      "total_elapsed": "01:45:30",
      "by_step": {
        "initialization": "00:00:15",
        "planning": "00:05:30",
        "execution": "01:35:00",
        "validation": "00:04:45"
      }
    },
    "resource_usage": {
      "total_cost": "$2.45",
      "token_usage": {
        "input_tokens": 15000,
        "output_tokens": 8000
      },
      "tool_calls": {
        "web_fetch": 8,
        "file_read": 12,
        "file_write": 5
      }
    },
    "quality_metrics": {
      "success_rate": 0.95,
      "error_rate": 0.05,
      "retry_rate": 0.10,
      "user_satisfaction": null
    }
  }
}
```

## State Persistence & Recovery

### Save Patterns
```yaml
automatic_saves:
  frequency: "after each step completion"
  triggers: ["step_transition", "error_occurrence", "user_pause"]
  location: "workspace/execution_state.md"
  
backup_strategy:
  interval: "every 10 minutes during execution"
  retention: "keep last 5 backups"
  location: "workspace/.backups/state_*.md"
```

### Recovery Patterns
```yaml
resume_execution:
  validation: "verify state consistency"
  recovery_point: "last successful step"
  context_restoration: "reload accumulated context"
  tool_state: "restore cached tool results"
  
rollback_capability:
  checkpoint_frequency: "major step boundaries"
  rollback_scope: "single step or full workflow"
  data_consistency: "ensure no partial updates"
```

## Integration with Training Data

### Training Data Enhancement
```json
{
  "training_integration": {
    "execution_trace": "complete step-by-step execution log",
    "decision_points": "agent decision rationale at each step",
    "context_evolution": "how context builds throughout execution",
    "error_patterns": "common failure modes and recoveries",
    "optimization_opportunities": "identified efficiency improvements",
    "user_interactions": "human intervention points and decisions"
  }
}
```

This execution state template provides the foundation for reliable, resumable, and analyzable workflow execution in LLMunix, enabling sophisticated state management and valuable training data generation.