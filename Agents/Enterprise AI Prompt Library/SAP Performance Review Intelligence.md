---
title: SAP Performance Review Intelligence
description: AI-powered analysis of employee performance reviews to identify trends, provide insights, and support fair evaluations
category: 
source: https://promptlib.nexgencompany.ai/
---
## SAP Performance Review Intelligence

AI-powered analysis of employee performance reviews to identify trends, provide insights, and support fair evaluations

## System Message

```
You are an AI assistant specialized in SAP performance review analysis. Your role is to:
1. Analyze performance data
2. Identify performance trends
3. Evaluate goal achievement
4. Assess competencies
5. Compare peer performance
6. Detect bias indicators
7. Recommend development areas
8. Generate review summaries

Use your knowledge of:
- SAP SuccessFactors Performance & Goals
- Performance evaluation methods
- Competency frameworks
- Goal setting and tracking
- Development planning
- Bias detection
- Performance metrics
- Review best practices

Ensure all analyses are fair, objective, and support employee development.
```

## User Message

```
Analyze the following performance review data and provide evaluation insights:

Input Data Sources:
1. Performance Data: {performance_data}
   Example format:
   {
     "employee_id": "EMP2024001",
     "review_period": "2023",
     "goals": [
       {
         "goal": "Increase team productivity",
         "target": "15% improvement",
         "achievement": "18% improvement",
         "evidence": [
           "Implemented new workflow",
           "Reduced processing time"
         ]
       }
     ],
     "competencies": [
       {
         "competency": "Leadership",
         "rating": 4,
         "examples": [
           "Led cross-functional project",
           "Mentored junior team members"
         ]
       }
     ]
   }

2. Historical Reviews: {history_data}
   Example format:
   {
     "previous_reviews": [
       {
         "period": "2022",
         "overall_rating": 3.8,
         "key_strengths": [
           "Technical expertise",
           "Team collaboration"
         ],
         "development_areas": [
           "Strategic thinking"
         ]
       }
     ]
   }

3. Team Context: {team_data}
   Example format:
   {
     "team_metrics": {
       "average_rating": 3.5,
       "performance_distribution": {
         "exceeds": 0.20,
         "meets": 0.60,
         "below": 0.20
       }
     },
     "department_goals": [
       {
         "goal": "Innovation",
         "target": "Launch 2 new initiatives",
         "achievement": "3 initiatives launched"
       }
     ]
   }

4. Development Plans: {development_data}
   Example format:
   {
     "current_plan": {
       "focus_areas": [
         "Leadership development",
         "Technical skills"
       ],
       "completed_training": [
         {
           "course": "Advanced Leadership",
           "completion_date": "2023-09",
           "impact": "HIGH"
         }
       ]
     }
   }

Expected Output Format:
{
  "performance_analysis": {
    "summary": {
      "employee_id": string,
      "overall_rating": number,
      "performance_trend": "IMPROVING | STABLE | DECLINING",
      "key_achievements": string[]
    },
    "detailed_assessment": {
      "goals": {
        "achievement_rate": number,
        "exceeded_goals": string[],
        "partially_met": string[],
        "impact_analysis": string[]
      },
      "competencies": {
        "strengths": [
          {
            "competency": string,
            "rating": number,
            "evidence": string[]
          }
        ],
        "development_areas": [
          {
            "competency": string,
            "rating": number,
            "recommendations": string[]
          }
        ]
      }
    },
    "comparative_analysis": {
      "peer_comparison": {
        "relative_position": string,
        "percentile": number,
        "distinguishing_factors": string[]
      },
      "historical_trend": {
        "rating_progression": number[],
        "growth_areas": string[],
        "consistent_strengths": string[]
      }
    },
    "recommendations": {
      "development_focus": [
        {
          "area": string,
          "importance": "HIGH | MEDIUM | LOW",
          "suggested_actions": string[],
          "expected_outcomes": string[]
        }
      ],
      "career_path": {
        "potential_roles": string[],
        "required_development": string[],
        "timeline": string
      }
    }
  }
}
```

## Example Output

```
{
  "performance_analysis": {
    "summary": {
      "employee_id": "EMP2024001",
      "overall_rating": 4.2,
      "performance_trend": "IMPROVING",
      "key_achievements": [
        "Exceeded productivity improvement target",
        "Successfully led cross-functional project",
        "Demonstrated strong mentorship capabilities"
      ]
    },
    "detailed_assessment": {
      "goals": {
        "achievement_rate": 0.95,
        "exceeded_goals": [
          "Team productivity improvement: 18% vs 15% target"
        ],
        "partially_met": [],
        "impact_analysis": [
          "Workflow improvements led to sustained efficiency gains",
          "Process optimization benefited entire department"
        ]
      },
      "competencies": {
        "strengths": [
          {
            "competency": "Leadership",
            "rating": 4,
            "evidence": [
              "Successfully led cross-functional project",
              "Effective mentoring of junior team members",
              "Proactive initiative in process improvements"
            ]
          }
        ],
        "development_areas": [
          {
            "competency": "Strategic Thinking",
            "rating": 3,
            "recommendations": [
              "Participate in strategic planning sessions",
              "Take on more long-term planning responsibilities",
              "Attend strategic thinking workshops"
            ]
          }
        ]
      }
    },
    "comparative_analysis": {
      "peer_comparison": {
        "relative_position": "Top 20%",
        "percentile": 85,
        "distinguishing_factors": [
          "Exceptional goal achievement rate",
          "Strong leadership capabilities",
          "Consistent performance improvement"
        ]
      },
      "historical_trend": {
        "rating_progression": [3.8, 4.2],
        "growth_areas": [
          "Leadership capabilities",
          "Process optimization skills"
        ],
        "consistent_strengths": [
          "Technical expertise",
          "Team collaboration"
        ]
      }
    },
    "recommendations": {
      "development_focus": [
        {
          "area": "Strategic Leadership",
          "importance": "HIGH",
          "suggested_actions": [
            "Enroll in advanced strategic management course",
            "Lead department-wide initiative",
            "Participate in strategy working groups"
          ],
          "expected_outcomes": [
            "Enhanced strategic decision-making",
            "Broader organizational impact",
            "Preparation for senior leadership role"
          ]
        }
      ],
      "career_path": {
        "potential_roles": [
          "Senior Team Lead",
          "Department Manager",
          "Strategic Projects Lead"
        ],
        "required_development": [
          "Strategic planning expertise",
          "Change management skills",
          "Advanced leadership capabilities"
        ],
        "timeline": "18-24 months"
      }
    }
  }
}
```

## Implementation Examples

```
from langchain.prompts import ChatPromptTemplate
from langchain.output_parsers import JSONOutputParser

# Create prompt template for performance review analysis
prompt_template = ChatPromptTemplate.from_messages([
    ("system", """You are an AI assistant specialized in SAP performance review analysis..."""),
    ("user", """Analyze the following performance review data and provide evaluation insights:
    
    Input Data Sources:
    1. Performance Data: {performance_data}
    2. Historical Reviews: {history_data}
    3. Team Context: {team_data}
    4. Development Plans: {development_data}
    """)
])

# Create chain with JSON output parser
chain = prompt_template | JSONOutputParser()

# Example usage
response = chain.invoke({
    "performance_data": {...},
    "history_data": {...},
    "team_data": {...},
    "development_data": {...}
})
```