# 1. LLM Parameter Extraction Validation Set

## (extraction_validation_data.json)
This repository contains a manually curated validation set used to evaluate LLM-based parameter extraction from scientific articles on graphene-based materials. The validation set was created from 40 articles, with five articles selected from each of eight topics identified previously by Latent Dirichlet Allocation (LDA) topic modeling.

For each article, relevant experimental parameters were manually identified and used as the ground truth. The LLM-extracted parameters were then compared against this manual annotation to evaluate whether the model correctly recovered the parameter name and its associated value.

## Topic Numbering

The `topic` field in each JSON record follows the numbering below:

| Topic ID | Topic |
|---:|---|
| 1 | Catalysis |
| 2 | Energy Storage |
| 3 | Polymer & Composite Reinforcement |
| 4 | Soft Matter & Scaffolds |
| 5 | Biomedical & Drug Delivery |
| 6 | Water Treatment & Membrane |
| 7 | Nanosensors |
| 8 | Films & Coatings |

## JSON Structure

Each article-level entry contains two main sections:

```json
{
  "info": {
    "doi": "10.1134/S0965544116060025",
    "llm_model_used": "kimi-k2-thinking",
    "topic": 1
  },
  "parameters": {
    "0": {
      "parameter_name": "graphite_mass",
      "evidence_text": "Twenty grams of natural graphite GK-1 and 10 g of NaNO3 were placed in a 2 L three-neck flask equipped with a mechanical stirrer and a thermometer; 550 mL of concentrated H2SO4 was poured into the flask.",
      "from_llm": true,
      "is_correct": true,
      "parameter_value": "20 g"
    }
  }
}
```

## Field Descriptions

### `info`

Article-level metadata.

| Field | Type | Description |
|---|---|---|
| `doi` | string | Digital Object Identifier of the scientific article. |
| `llm_model_used` | string | Name of the LLM used to perform the parameter extraction. |
| `topic` | integer | LDA topic assigned to the article, using the topic numbering defined above. |

### `parameters`

Dictionary containing the manually validated parameter records for the article. Each key, such as `"0"`, `"1"`, or `"2"`, is an internal parameter index.

| Field | Type | Description |
|---|---|---|
| `parameter_name` | string | Name assigned to the extracted parameter. |
| `parameter_value` | string | Value associated with the parameter, usually a numerical value with units when available. |
| `evidence_text` | string | Text span from the article supporting the parameter annotation or extraction. |
| `from_llm` | boolean | Indicates whether the LLM found and extracted this parameter. |
| `is_correct` | boolean | Indicates whether the LLM correctly extracted both the parameter name and the parameter value, according to the manual validation. |

## Validation Interpretation

The manual annotations serve as the ground truth. A parameter is considered correctly extracted only when the LLM identifies the relevant parameter and assigns the correct corresponding value. In this validation setting:

- A true positive corresponds to a parameter correctly extracted by the LLM and confirmed by the manual annotation.
- A false positive corresponds to a parameter extracted by the LLM that was not accepted as correct during manual validation.
- A false negative corresponds to a manually annotated parameter that was missed by the LLM.

This structure was used to evaluate the performance of the LLM extraction pipeline across the eight LDA-derived graphene-based materials topics.

# 2. 

## (xxxx.json)

# 3. Parameter Communities Recommendation

# 3. Parameter Communities Recommendation

One JSON file is provided:

- `recommend_system_lookup_table.json`: contains the probability that a given parameter community is relevant given a topic and a material cotegory.


## JSON Structure

Each entry contains a dictionary with five keys: <code>{'topic', 'material', 'community', 'probability', 'parameters'}</code>. Since there are 8 topics, 9 material categories, and 32 parameter communities, the dataset contains 2,304 entries.  Probabilities close to zero indicate that a given parameter community is not frequently reported in association with that topic and material class.

```json
[
    {
        "topic": "Catalysis",
        "material": "Non-graphene-based target",
        "community": "C1",
        "probability": 0.7747933884297521,
        "parameters": [
            "substrate_dimensions",
            "membrane_thickness",
            "water_cement_ratio",
            "degassing_time",
            "interlayer_spacing",
            "coating_thickness",
            "surface_roughness",
            "immersion_time",
            "water_flux",
            "filtration_pressure",
            "curing_time",
            "water_contact_angle",
            "operating_pressure",
            "curing_temperature",
            "simulation_temperature",
            "effective_membrane_area",
            "substrate_material"
        ]
    },...
```

### Field Descriptions


| Field | Type | Description |
|---|---|---|
| `topic` | string | Topic $t_i$ . |
| `material` | string | Material category $\Omega_i$. |
| `community` | string | Community $c_i$. |
| `probability` | float | The conditional probability of observing parameter community $c_i$ given topic $t_i$ for material category $\Omega_i$. |
| `parameters` | list | List of parameters (strings) for that community. |


## (recommend_system_lookup_table.json)
