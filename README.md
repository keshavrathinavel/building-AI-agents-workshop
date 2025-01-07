# Building

**Steps**

1. Overall System Architecture
    1. One manager agent to oversee the process
    2. 3 Specialist agents
        1. Classifier
        2. Router
        3. Responder
    3. Sequential workflow where tickets flow through these agents
        1. Input ticket → Supervisor
        2. Supervisor → Classifier (get category/priority)
        3. Supervisor → Router (get department)
        4. Supervisor → Responder (draft response)
        5. Supervisor reviews and outputs final result
2. Agent Definitions
    1. Supervisor Agent
        1. Role: Coordinate the workflow between agents
        2. Skills: Process management, delegation, quality control
        3. Tools needed: Access to all ticket information, ability to call other agents
    2. Classifier Agent
        1. Role: Initial ticket analysis
        2. Skills: Categorisation, priority assessment, key info extraction
        3. Tools needed: Classification prompt templates, category definitions
        4. Outputs: Ticket category, priority level, key extracted information
        
        ```python
        - analyze_ticket_content() -> Extracts key information from ticket text
        - determine_priority() -> Assigns priority based on content
        - identify_category() -> Maps ticket to predefined categories
        ```
        
    3. Router Agent
        1. Role: Determine best department/handler
        2. Skills: Department matching, workload assessment
        3. Tools needed: Department rules/criteria, current workload info
        4. Outputs: Target department, routing justification
        
        ```python
        - check_department_load() -> Checks current ticket load per department
        - match_skills_required() -> Maps ticket needs to department capabilities
        - get_routing_rules() -> Retrieves current routing policies
        ```
        
    4. Responder Agent
        1. Role: Draft initial responses
        2. Skills: Response composition, template customisation
        3. Tools needed: Response templates, knowledge base access
        4. Outputs: Draft response, suggested knowledge base articles
        
        ```python
        - fetch_knowledge_base_articles() -> Gets relevant help articles
        - generate_response() -> Creates custom response
        - check_response_tone() -> Ensures appropriate tone
        ```
        
3. Assign tools to agents like so:
    
    ```python
    Copyclassifier_agent = Agent(
        role="Classifier",
        goal="Accurately categorize support tickets",
        tools=[analyze_ticket_content, determine_priority, identify_category]
    )
    ```
