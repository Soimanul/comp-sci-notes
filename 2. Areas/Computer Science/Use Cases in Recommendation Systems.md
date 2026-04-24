**Tags:** #concept #reco
**Related:** [[Recommendation System Overview]], [[Business Value of Recommendations]], [[Cold Start Problem]]

## Definition

**Use cases in recommendation systems** are the specific business applications where a reco is deployed, each characterised by the type of items, user data available, difficulty to implement, and expected ROI.

> [!info] Key Intuition
> The same underlying recommendation engine can be applied across retail, gaming, food, media, and travel — but each domain has different data availability, user intent, and business constraints that affect design choices.

## Use Cases by Industry

### Retail
| Task | Difficulty | ROI |
|---|---|---|
| Personalized recommendation | Medium | High |
| You might also like (upselling) | Medium | High |
| Frequently bought together (cross-selling) | Medium | High |
| Similar alternatives (downselling) | Medium | High |
| Visual recommendation | High | High |
| Shopping assistant (chatbot) | Low | Medium |

### Gaming
| Task | Difficulty | ROI |
|---|---|---|
| Personalized game recommendation | Medium | Medium |
| Personalized item recommendation | Medium | High |
| Next best action prediction | High | Low |
| People you may know | Medium | Medium |
| Adaptive gameplay | High | Low |

### Food & Restaurants
| Task | Difficulty | ROI |
|---|---|---|
| Geolocation-based recommendation | Medium | High |
| Personalized recommendation | Medium | High |
| Cross-selling | Medium | High |
| Personalised loyalty program | Medium | Medium |
| Support assistant (chatbot) | Low | High |

### Media & Entertainment
| Task | Difficulty | ROI |
|---|---|---|
| Written content recommendation | Medium | High |
| Video recommendation | High | High |
| Music recommendation | High | High |
| Event-based recommendation | Medium | High |
| Personal assistant (chatbot) | Low | Medium |

### Travel & Leisure
| Task | Difficulty | ROI |
|---|---|---|
| Geolocation recommendation | Medium | High |
| Activity recommendation | Medium | High |
| Personalized item recommendation | Medium | High |
| Trip itinerary recommendation | High | Medium |
| Travel assistant (chatbot) | Low | High |

> [!warning] Common Misconception
> Visual recommendation (image-based) appears in every industry's high-ROI list but is consistently rated **High difficulty**. This is because it requires multi-modal data pipelines and more complex models, not just collaborative filtering.

## Significance

Understanding use cases before choosing a model is critical: a chatbot assistant has Low difficulty but Medium ROI, while visual recommendations have High difficulty but High ROI. Engineering decisions must weigh these trade-offs.
