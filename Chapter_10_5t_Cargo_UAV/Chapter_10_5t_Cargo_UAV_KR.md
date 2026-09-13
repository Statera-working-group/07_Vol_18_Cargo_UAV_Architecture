**Volume 18. Cargo UAV Architecture**

# Chapter 10. 5t Cargo UAV

## 10.01. Hybrid Electric Architecture

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

5톤급 화물 무인항공기(Cargo UAV)에는 이륙과 상승 과정에서 요구되는 높은 순간 출력(Peak Power)을 지원하는 동시에 지역 간 화물 운송 임무에 필요한 충분한 에너지 용량(Energy Capacity)을 확보해야 하므로 하이브리드 전기 아키텍처(Hybrid-Electric Architecture)가 필요하다. 항공기의 크기와 임무 거리가 증가할수록 순수 배터리 전기 시스템(Pure Battery-Electric System)은 배터리 질량의 증가로 인해 제약을 받게 된다. 하이브리드화(Hybridization)는 최대 출력과 지속 에너지 요구조건을 분리하여 각 운용 조건에 적합한 에너지원을 최적화할 수 있도록 한다.

이 아키텍처는 일반적으로 주 에너지원(Primary Energy Source), 전력 생성 시스템(Electrical Generation System), 고전압 직류 배전망(High-Voltage DC Distribution Network), 배터리 에너지 저장 시스템(Battery Energy-Storage System), 추진 인버터(Propulsion Inverter), 전기 모터(Electric Motor), 에너지 관리 시스템(Energy Management System, EMS)을 중심으로 구성된다. 연료 기반 발전 시스템은 순항에 필요한 지속적인 에너지를 공급하고, 배터리는 순간적인 출력 요구와 급격한 부하 변화를 담당한다. 전기 버스(Electrical Bus)는 발전, 저장, 추진, 항공전자 및 보조 부하를 연결하는 핵심 에너지 백본(Energy Backbone)이 된다.

직렬형 하이브리드 전기 구성(Series Hybrid-Electric Configuration)은 기계적 추진과 열에너지 기반 발전 기능을 분리할 수 있기 때문에 자율 화물 항공기(Autonomous Cargo Aircraft)에 특히 적합하다. 터빈(Turbine) 또는 내연기관(Internal-Combustion Engine)은 프로펠러를 직접 구동하는 대신 하나 이상의 발전기(Generator)를 구동한다. 생성된 전력은 고전압 네트워크를 통해 조정 및 분배되어 독립적인 추진 채널(Propulsion Channel)에 공급되므로 복잡한 기계식 동력전달장치 없이도 모터를 유연하게 배치하고 분산 전기 추진(Distributed Electric Propulsion)을 구현할 수 있다.

고전압 직류 버스(High-Voltage DC Bus)는 도체 질량을 최소화하고 허용 가능한 수준의 전력 손실을 유지하면서 대용량 추진 부하를 처리해야 한다. 배전 전압을 높이면 동일한 전력에서 전류를 감소시킬 수 있으므로 케이블 단면적과 저항 손실을 줄일 수 있다. 그러나 높은 전압은 절연 협조(Insulation Coordination), 연면거리 및 공간거리(Creepage and Clearance), 커넥터 설계(Connector Design), 아크 보호(Arc Protection), 전자파 적합성(Electromagnetic Compatibility), 절연 감시(Isolation Monitoring), 안전 정비 절차(Safe Maintenance Procedure)에 대해 더욱 엄격한 요구조건을 발생시킨다.

배터리 팩(Battery Pack)은 하이브리드 아키텍처에서 단순한 에너지 저장장치 이상의 역할을 수행한다. 배터리는 수직 이륙, 가속, 상승, 기동, 발전기 과도상태(Generator Transient), 비상 운용 시 전력 버퍼링(Power Buffering)을 제공한다. 순항 중에는 발전기가 효율적인 운전점(Operating Point) 부근에서 동작하고, 열 상태와 충전 상태(State of Charge, SOC)가 허용하는 경우 잉여 전력으로 배터리를 충전할 수 있다. 이러한 구성은 짧은 시간 동안 발생하는 최대 추진 출력만을 기준으로 발전기 용량을 과도하게 설계하는 것을 방지한다.

추진 전력(Propulsion Power)은 전기적으로 절연되거나 독립적으로 보호되는 여러 채널로 분할하는 것이 바람직하다. 각 채널은 자체 접촉기(Contactor), 보호장치(Protection Device), 인버터(Inverter), 모터 제어기(Motor Controller), 추진 모터(Propulsion Motor)를 포함할 수 있다. 따라서 단일 버스 또는 인버터 고장이 모든 추력원을 동시에 상실시키지 않도록 설계해야 한다. 교차 연결 접촉기(Cross-Tie Contactor)를 통해 정상 채널 사이에서 제한적인 에너지 공유가 가능하지만, 전기적 고장의 전파를 방지하도록 고장 격리 로직(Fault-Containment Logic)에 의해 제어되어야 한다.

발전 서브시스템(Generation Subsystem) 역시 최대 효율만이 아니라 이중화(Redundancy)를 중심으로 설계되어야 한다. 하나의 중앙 집중식 발전기보다 여러 개의 소형 발전 채널을 사용하는 방식이 시스템 질량과 복잡성을 증가시킬 수 있지만 더 높은 고장 허용성(Fault Tolerance)을 제공할 수 있다. 발전기 제어기(Generator Controller)는 전압, 전류, 회전속도 및 열 한계를 조절하면서 항공기 수준의 에너지 관리 시스템과 협조한다. 발전기 하나가 고장 나면 신속하게 격리하고, 나머지 발전원과 배터리가 필수 추진 및 항공전자 부하를 자동으로 지원해야 한다.

에너지 관리 시스템(Energy Management System)은 발전기, 배터리, 추진 장치 및 보조 시스템 사이에서 전력을 어떻게 분배할 것인지를 지속적으로 결정한다. 이러한 결정에는 비행 단계(Flight Phase), 요구 추력(Requested Thrust), 배터리 충전 상태, 배터리 온도, 발전기 가용 출력, 예상 임무 에너지(Predicted Mission Energy), 예비 에너지 요구조건(Reserve Requirement), 감지된 고장 상태 등이 반영된다. 고급 제어 시스템은 단순히 순간적인 전력 요구에 반응하는 것이 아니라 임무 계획 정보를 이용하여 향후 상승, 순항, 하강, 착륙 및 대체 경로 운항에 필요한 에너지를 사전에 예측할 수 있다.

이륙(Takeoff)은 가장 높은 전력 요구가 발생하는 운용 상태 가운데 하나이다. 발전기는 연속 출력 또는 단시간 출력 한계 부근에서 운전되고, 배터리는 추진 네트워크에 추가적인 최대 전력(Peak Power)을 공급할 수 있다. 항공기가 효율적인 전진 비행(Forward Flight) 상태로 전환되면 추진 전력 요구가 감소하고 시스템은 발전기 중심 운전(Generator-Dominant Operation)으로 전환될 수 있다. 이후 배터리 충전 상태를 점진적으로 회복하여 착륙, 복행(Go-Around), 비상 우회 운항(Emergency Diversion)에 필요한 충분한 전기 에너지 예비량을 확보할 수 있다.

이 정도 출력 수준에서는 열 관리(Thermal Management)를 전기 아키텍처와 분리하여 생각할 수 없다. 발전기, 정류기(Rectifier), 직류 변환기(DC/DC Converter), 배터리, 인버터, 모터 및 대전류 배전 부품은 모두 열을 발생시킨다. 독립적이거나 부분적으로 분리된 냉각 루프(Cooling Loop)는 단일 열관리 시스템의 고장이 여러 추진 채널을 동시에 정지시키는 것을 방지할 수 있다. 따라서 온도 측정값은 전력 관리에 직접 반영되어야 하며, 구성요소의 온도가 파괴적이거나 위험한 수준에 도달하기 전에 제어된 출력 제한(Controlled Derating)을 수행할 수 있어야 한다.

저전압 전기 영역(Low-Voltage Electrical Domain)은 추진용 고전압 영역(High-Voltage Propulsion Domain)과 기능적으로 분리되어야 한다. 절연형 직류 변환기(Isolated DC/DC Converter)는 비행제어 컴퓨터(Flight-Control Computer), 항공전자 장비(Avionics), 통신 장비, 항법 센서(Navigation Sensor), 화물 관리 전자장치(Cargo-Management Electronics), 액추에이터(Actuator), 안전 시스템에 전원을 공급할 수 있다. 핵심 항공전자 시스템에는 이중화된 전원 공급과 독립적인 백업 에너지가 필요하며, 주 추진 버스의 손실이 비행제어 권한, 항법 기능 또는 지휘·통제 통신(Command-and-Control Communication)의 즉각적인 상실로 이어져서는 안 된다.

고장 관리(Fault Management)는 전기적 보호 기능과 비행제어 동작을 상호 연계해야 한다. 과전류(Overcurrent), 절연 고장(Isolation Failure), 인버터 고장, 배터리 열 이상(Battery Thermal Event), 발전기 상실, 비정상 버스 전압, 냉각 성능 저하 또는 통신 장애가 발생하면 사전에 정의된 격리 및 재구성(Isolation and Reconfiguration) 동작이 실행되어야 한다. 동시에 비행제어 시스템은 변화된 추진 능력을 파악하여 추력 배분, 비행 궤적, 속도, 고도, 착륙지 선정 및 임무 지속 여부를 실제 사용 가능한 전력과 일치하도록 결정해야 한다.

물리적 분리(Physical Separation)는 논리적 이중화(Logical Redundancy)만큼 중요하다. 이중화된 고전압 케이블, 접촉기, 배터리 모듈, 통신 링크 및 냉각 회로가 불필요하게 동일한 경로를 공유하면 화재, 충격, 유체 누출 또는 구조적 손상 하나로 여러 채널이 동시에 상실될 수 있다. 따라서 전기 구역(Electrical Zone)을 항공기의 구조적 구역(Structural Zone)과 연계하여 분산형 에너지 아일랜드(Distributed Energy Island)를 구성하면 고장을 국부적으로 격리하면서 정상 영역이 제어 비행에 필요한 충분한 전력을 계속 공급하도록 설계할 수 있다.

하이브리드 아키텍처는 추진 제어(Propulsion Control)와 화물 운용(Cargo Operation) 사이에도 긴밀한 인터페이스를 형성한다. 탑재화물 질량(Payload Mass)과 무게중심(Center of Gravity, CG) 정보는 요구 추력, 임무 에너지, 상승 성능 및 예비 에너지 계산에 영향을 준다. 출발 전에 항공기는 측정된 화물 조건을 비행거리, 기상 가정, 배터리 상태, 연료 가용량, 발전기 건전성 및 추진 시스템 이중화 상태와 결합하여 정의된 비상 조건에서도 충분한 에너지 여유도(Energy Margin)를 유지할 수 있는지 판단할 수 있다.

따라서 5톤급 화물 무인항공기의 하이브리드 전기 아키텍처(Hybrid-Electric Architecture)는 단순히 엔진과 배터리를 결합한 시스템이 아니라 통합된 항공기 수준 에너지 및 안전 시스템(Aircraft-Level Energy and Safety System)으로 다루어야 한다. 발전, 에너지 저장, 고전압 배전, 추진, 냉각, 항공전자 전원, 고장 격리 및 임무 계획이 상호 조정되는 계층으로 동작해야 한다. 이러한 시스템 수준 접근법(System-Level Approach)은 이후 다루게 될 항속거리 연장 설계(Extended-Range Design), 항공전자 아키텍처(Avionics Architecture), 지역 물류 통합(Regional Logistics Integration), 인증 계획(Certification Planning)의 기반을 제공한다.

## 10.02. Extended Range Design

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

5톤급 화물 무인항공기(Cargo UAV)의 항속거리 연장 설계(Extended-Range Design)는 단순히 배터리 용량을 증가시키는 것만으로는 임무 지속시간을 효율적으로 늘릴 수 없다는 인식에서 시작된다. 배터리 모듈을 추가할 때마다 저장 전기에너지는 증가하지만 동시에 이륙 중량, 구조 하중, 요구 양력 및 추진 출력도 증가한다. 따라서 하이브리드 전기 항공기(Hybrid-Electric Aircraft)는 높은 비에너지(Specific Energy)를 가진 연료와 최대 출력, 과도 응답, 예비 능력 및 비상 운용에 최적화된 배터리를 결합하여 항속거리를 확장한다.

항속거리(Range)는 단순한 연료 용량 문제가 아니라 항공기 수준의 에너지 문제(Aircraft-Level Energy Problem)로 다루어야 한다. 탑재화물 질량(Payload Mass), 공력 효율(Aerodynamic Efficiency), 순항 속도, 고도, 추진 효율, 발전기 효율, 배터리 상태, 기상 조건, 예비 에너지 요구조건 및 우회 비행거리가 모두 실제 임무 반경에 영향을 준다. 따라서 설계 목표는 비정상 및 비상 조건에 충분한 여유도를 유지하면서 운송되는 화물 단위당 총 에너지 소비를 최소화하는 것이다.

실용적인 항속거리 연장 아키텍처(Extended-Range Architecture)는 지속 비행 중 연료를 주 에너지원으로 사용하면서 항공기 전체에는 전기 추진(Electrical Propulsion)을 유지할 수 있다. 터빈(Turbine) 또는 엔진(Engine)이 발전기(Generator)를 구동하고, 생성된 전력은 정류(Rectification) 및 고전압 배전(High-Voltage Distribution)을 거쳐 추진 인버터와 모터에 공급된다. 배터리는 동적 에너지 버퍼(Dynamic Energy Buffer)로 전기 네트워크에 연결되어 열기관 기반 발전기가 보다 좁고 효율적인 운전 영역에서 동작하도록 한다.

임무 에너지(Mission Energy)는 수직 이륙, 전환 비행(Transition), 상승, 순항, 하강 및 착륙 과정에서 요구 출력이 크게 달라지므로 비행 단계(Flight Phase)에 따라 구분해야 한다. 이륙과 상승은 비교적 짧은 시간 동안 높은 추진 출력을 요구하지만 순항은 훨씬 긴 시간 동안 상대적으로 낮은 출력을 요구한다. 발전기를 지속 순항 및 연속 비행 요구조건에 맞추고 배터리를 일시적인 최대 부하에 활용하면 발전기의 과도한 대형화를 줄이고 항공기 전체의 질량 효율을 향상시킬 수 있다.

임무 거리가 증가할수록 순항 최적화(Cruise Optimization)는 특히 중요해진다. 공기저항, 프로펠러 효율, 모터 효율, 인버터 효율 또는 발전기 효율의 작은 개선도 장시간 운항 과정에서 누적된다. 따라서 순항 속도는 반드시 항공기의 최대 속도와 일치할 필요가 없다. 바람직한 운전점은 임무시간 요구조건을 충족하면서 에너지 소비를 최소화할 수 있는 대기속도, 고도, 추진 부하 및 발전기 출력의 에너지 효율적인 조합이다.

에너지 관리 시스템(Energy Management System, EMS)은 현재 사용 가능한 에너지뿐만 아니라 남은 항로에 필요한 예상 에너지까지 계산해야 한다. 비행계획 거리, 항공기 질량, 고도 프로파일, 예상 바람, 추진 효율, 배터리 충전 상태(State of Charge, SOC), 연료량 및 발전기 건전성을 결합하여 향후 에너지 여유도(Energy Margin)를 추정할 수 있다. 이를 통해 에너지 관리는 단순한 반응형 전력 균형 제어에서 자율적인 항속거리 판단을 지원하는 예측형 임무 에너지 관리(Predictive Mission-Energy Management)로 발전한다.

배터리 충전 상태(State of Charge)는 가능한 최고 수준으로 단순 유지하는 것이 아니라 임무에 따라 정의된 운용 범위(Mission-Dependent Operating Window) 내에서 제어해야 한다. 고출력 비행 단계에서는 배터리를 제어된 방식으로 방전하여 발전기 출력을 보조한다. 효율적인 순항 중에는 사용 가능한 발전기 용량을 이용해 소비된 배터리 에너지의 일부를 회복할 수 있다. 하강과 착륙 전에는 접근, 착륙, 복행(Go-Around), 발전기 고장, 통신 두절 복구 또는 대체 착륙지로의 우회에 필요한 충분한 충전량을 유지해야 한다.

연료 용량(Fuel Capacity) 역시 최대화하는 것이 아니라 최적화해야 한다. 추가 연료는 잠재적인 비행 지속시간을 증가시키지만 항공기 질량을 증가시키며, 이는 다시 요구 양력과 에너지 소비를 증가시킨다. 따라서 연료탱크 크기와 위치, 구조 보강, 연료 펌핑 장치, 화재 보호 및 변화하는 무게중심(Center of Gravity, CG)을 함께 평가해야 한다. 사용 가능한 연료량은 단순히 가용 구조 공간을 모두 채우는 방식이 아니라 정의된 임무 프로파일과 예비 연료 정책을 기반으로 결정해야 한다.

화물과 연료가 모두 항공기 질량의 상당 부분을 차지하면 무게중심 변화(Center-of-Gravity Variation)가 중요해진다. 연료가 소비되면서 항공기의 무게중심이 이동할 수 있으며 이는 안정성, 제어 요구량, 공력 트림(Aerodynamic Trim), 추진 효율에 영향을 준다. 연료탱크 배치와 연료 이송 전략(Fuel-Transfer Strategy)을 통해 이러한 영향을 감소시킬 수 있다. 또한 연료 사용 순서 제어 또는 능동 이송(Active Transfer)을 이용하여 임무 전반에 걸쳐 무게중심을 에너지 효율적이고 제어 가능한 영역 내에 유지할 수 있다.

항속거리 연장 운용(Extended-Range Operation)에서는 상당한 에너지가 이미 소비된 이후에도 추진 이중화(Propulsion Redundancy)가 유효하게 유지되어야 한다. 목적지에 도착할 때 전기 또는 연료 예비량이 거의 남지 않는 정상 임무는 운용적으로 강건하지 않다. 따라서 항속거리 계산에는 이상적인 비행경로뿐만 아니라 발전기 상실, 추진 채널 성능 저하, 예상치 못한 역풍, 체공(Holding), 경로 변경, 착륙 중단, 복행 및 대체 착륙지 회복을 위한 비상 에너지도 포함해야 한다.

열 조건(Thermal Condition)은 실제 운용 가능한 항속거리를 직접 감소시킬 수 있다. 발전기의 연속 운전, 지속적인 인버터 부하, 모터 발열, 배터리 충방전 및 높은 외기 온도로 인해 충분한 연료가 남아 있더라도 출력 제한(Power Derating)이 발생할 수 있다. 따라서 냉각 시스템 능력은 전체 임무 지속시간에 걸쳐 평가되어야 한다. 열 예측(Thermal Prediction)을 에너지 관리에 통합하면 단기적인 성능 확보를 위해 이후의 추진 가용성을 희생하는 운용 전략을 방지할 수 있다.

장시간 임무에서는 배전 손실(Electrical Distribution Loss) 역시 중요해진다. 고전압 운용은 전류와 도체 손실을 감소시키며, 고효율 변환기, 짧은 전력 경로, 최적화된 케이블 크기 및 고효율 인버터는 누적되는 에너지 손실을 줄인다. 그러나 아키텍처는 이론적인 전송 효율만을 기준으로 버스 전압을 선정해서는 안 되며 전기 효율과 절연 질량, 보호 요구조건, 전자파 적합성(Electromagnetic Compatibility), 정비성 및 고장 격리(Fault Containment)를 함께 고려해야 한다.

탑재화물-항속거리 절충(Payload-Range Tradeoff)은 5톤급 화물 무인항공기의 핵심 특성이다. 탑재화물, 연료, 배터리 및 항공기 구조가 허용 이륙중량 내에서 서로 경쟁하기 때문에 일반적으로 최대 탑재량과 최대 항속거리를 동시에 달성할 수 없다. 따라서 임무 계획에서는 화물 질량과 비행거리의 실행 가능한 조합을 나타내는 탑재화물-항속거리 영역(Payload-Range Envelope)을 사용해야 한다. 이를 통해 물류 시스템은 화물량을 줄일지, 중간 기착지를 추가할지 또는 다른 항공기를 투입할지를 판단할 수 있다.

항로 계획(Route Planning)을 최적화하면 항공기 하드웨어를 변경하지 않고도 운용 항속거리를 추가로 확장할 수 있다. 바람을 고려한 경로 설정, 고도 최적화, 에너지 효율적인 상승 프로파일, 호버링(Hover) 시간 단축, 전환 시점 최적화 및 적절한 우회 착륙지 선정은 전체 임무 에너지를 감소시킬 수 있다. 자율 운항에서는 기상, 공역 제한, 항공기 건전성 및 목적지 조건이 변화함에 따라 이러한 계산을 지속적으로 갱신하여 에너지 여유도가 위험 수준에 도달하기 전에 비행 전략을 변경할 수 있다.

궁극적으로 항속거리 연장 설계(Extended-Range Design)는 추진 아키텍처, 에너지 저장, 공기역학(Aerodynamics), 열 관리, 화물 적재, 비행 계획 및 안전을 하나의 통합 최적화 문제(Integrated Optimization Problem)로 연결한다. 5톤급 화물 무인항공기의 목표는 단순히 가능한 한 멀리 비행하는 것이 아니라 예측 가능한 에너지 예비량과 고장 허용성(Fault Tolerance)을 유지하면서 지역 간 거리에 걸쳐 유용한 화물을 운송하는 것이다. 이러한 아키텍처는 이후 다루게 될 항공전자 시스템(Avionics), 지역 물류(Regional Logistics) 및 인증(Certification)을 위한 에너지 기반을 제공한다.

## 10.03. 5t Avionics Architecture

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

5톤급 화물 무인항공기(Cargo UAV)에는 비행제어(Flight Control), 항법(Navigation), 추진 협조(Propulsion Coordination), 에너지 관리(Energy Management), 통신(Communication), 화물 감시(Cargo Supervision), 안전 기능(Safety Function)을 고장 허용형 항공 컴퓨팅 환경(Fault-Tolerant Airborne Computing Environment)으로 통합하는 항공전자 아키텍처(Avionics Architecture)가 필요하다. 소형 무인항공기보다 큰 운동에너지, 높은 화물 가치, 대규모 전력 및 운용 책임을 가지므로 항공전자 시스템의 가용성(Availability)과 결정론적 동작(Deterministic Behavior)은 부수적인 장비 특성이 아니라 항공기 수준의 핵심 요구조건이 된다.

아키텍처는 안전 필수 비행 기능(Safety-Critical Flight Function)과 임무 중심 컴퓨팅(Mission-Oriented Computing)을 분리하면서 이들 사이에 통제된 인터페이스(Controlled Interface)를 유지해야 한다. 비행제어 컴퓨터(Flight Control Computer, FCC)는 안정화, 유도, 액추에이터 명령 및 비행영역 보호(Flight-Envelope Protection)를 수행하고, 임무 컴퓨터(Mission Computer)는 항로 실행, 물류 정보, 탑재체 기능 및 상위 수준 자율 기능을 담당한다. 이러한 분리는 임무 애플리케이션의 연산 과부하나 고장이 안전한 비행을 유지하는 데 필요한 결정론적 제어 루프에 직접적인 영향을 주는 것을 방지한다.

비행제어 컴퓨팅(Flight-Control Computing)은 개별 고장을 감지하고 고장 이후에도 제어를 유지할 수 있는 이중화 채널(Redundant Channel)을 적용해야 한다. 여러 프로세서는 동기화된 센서 입력을 이용하여 항공기 상태와 제어 명령을 독립적으로 계산할 수 있다. 계산 결과는 추진 및 비행제어 액추에이터에 명령이 전달되기 전에 감시 또는 보팅 로직(Voting Logic)을 통해 비교할 수 있다. 채널 독립성(Channel Independence)은 전원, 통신, 시간 동기화 및 소프트웨어까지 포함하여 명목상의 이중화가 공통원인 고장(Common-Mode Failure) 경로를 숨기지 않도록 해야 한다.

항법 아키텍처(Navigation Architecture)는 모든 운용 조건에서 하나의 센서만으로 신뢰성을 유지할 수 없으므로 상호 보완적인 센서 기술을 결합한다. 이중화된 관성측정장치(Inertial Measurement Unit, IMU), 위성항법시스템(GNSS) 수신기, 대기자료 센서(Air-Data Sensor), 레이더 또는 전파고도 정보(Radio-Altitude Information), 기타 항법원을 융합하여 위치, 속도, 자세, 고도 및 방위각을 추정할 수 있다. 센서 불일치 감시(Sensor Disagreement Monitoring)를 통해 성능이 저하된 측정값을 식별하고 자율 비행 능력을 즉시 상실하지 않으면서 항법 시스템을 재구성할 수 있다.

정확한 시간 동기화(Time Synchronization)는 비행제어, 항법, 추진, 인지(Perception), 건전성 감시(Health Monitoring) 데이터가 분산된 장치에서 생성되기 때문에 필수적이다. 센서 측정값에는 신뢰할 수 있는 타임스탬프(Timestamp)가 포함되어야 하며, 이를 통해 센서 융합 알고리즘이 동일한 물리적 상태를 나타내는 관측값을 비교할 수 있다. 공통 항공기 시간 기준(Common Aircraft Time Base)은 시스템 이벤트의 일관된 순서를 제공하여 이벤트 재구성, 고장 진단, 비행 데이터 기록, 정비 분석 및 인증 근거(Certification Evidence)의 신뢰성을 향상시킨다.

항공전자 통신 네트워크(Avionics Communication Network)는 결정론적인 안전 통신(Deterministic Safety Traffic)과 고대역폭 임무 및 센서 데이터(High-Bandwidth Mission and Sensor Data)를 구분해야 한다. 비행제어 명령, 액추에이터 피드백, 추진 상태 및 핵심 건전성 정보에는 예측 가능한 지연시간과 제한된 전송 동작이 필요하다. 카메라, 라이다(LiDAR), 기상 정보, 지도, 화물 데이터 및 진단 기록은 훨씬 높은 대역폭을 요구할 수 있지만 일반적으로 서로 다른 시간 특성을 허용할 수 있다. 네트워크 분할(Network Partitioning)을 통해 비필수 통신이 비행 필수 통신을 방해하지 않도록 해야 한다.

단일 스위치, 케이블, 인터페이스 또는 전원 영역의 상실로 핵심 항공전자 장비가 고립될 가능성이 있는 경우 이중화된 네트워크 경로(Redundant Network Path)가 필요하다. 독립적인 통신 채널은 비행 컴퓨터, 항법 장치, 추진 제어기 및 원격 입출력 모듈(Remote I/O Module)을 연결할 수 있다. 게이트웨이 기능(Gateway Function)은 안전 필수 영역과 임무 영역 사이를 이동하는 데이터를 엄격하게 통제해야 하며 메시지 검증, 전송률 제한, 송신원 인증, 고장 필터링 및 적절한 사이버보안(Cybersecurity) 제어를 포함해야 한다.

추진 항공전자 시스템(Propulsion Avionics)은 하이브리드 전기 동력 아키텍처(Hybrid-Electric Power Architecture)와 긴밀하게 협조해야 한다. 비행제어 시스템은 요구 추력을 결정하고 추진 제어기(Propulsion Controller)는 이를 모터 토크, 회전속도 및 인버터 명령으로 변환한다. 동시에 에너지 관리 시스템(Energy Management System, EMS)은 발전기와 배터리에서 사용할 수 있는 전력을 결정한다. 전력 한계와 추진 가용 능력을 지속적으로 교환하면 에너지원, 모터, 인버터 또는 냉각 시스템의 성능이 저하된 경우에도 비행 명령이 실제 구현 가능한 범위 내에서 유지될 수 있다.

따라서 항공전자 아키텍처는 모든 구성요소 고장을 즉각적인 임무 종료 상황으로 처리하기보다 점진적 성능 저하(Graceful Degradation)를 지원해야 한다. 하나의 추진 채널을 사용할 수 없게 되면 비행제어기는 설정된 제어 한계 내에서 정상 추진 장치로 추력을 재분배할 수 있다. 발전기가 고장 나면 에너지 관리 시스템이 가용 출력을 다시 계산할 수 있다. 항법 품질이 저하되면 대체 센서 조합을 선택하고 임무 관리 시스템(Mission Manager)은 임무 지속, 우회 또는 착륙 가운데 적절한 대응을 판단할 수 있다.

전용 기체 건전성 관리 기능(Vehicle Health Management)은 비행 컴퓨터, 전력전자 장치, 배터리, 발전기, 모터, 액추에이터, 센서, 통신 네트워크, 냉각 시스템 및 화물 장비의 상태 정보를 수집할 수 있다. 단순히 개별 진단 코드(Diagnostic Code)를 표시하는 것이 아니라 서브시스템 사이의 이벤트를 상호 연관시켜 분석해야 한다. 이를 통해 항공기는 국부적인 센서 이상과 시스템 수준으로 발전하고 있는 이상 상태를 구분할 수 있으며, 장기간의 기단 운용(Fleet Operation)을 통해 축적된 데이터를 기반으로 예지정비(Predictive Maintenance)를 지원할 수 있다.

화물 항공전자 시스템(Cargo Avionics) 역시 중요한 영역을 구성하는데, 이는 탑재화물 상태가 항공기 운용에 직접적인 영향을 미치기 때문이다. 중량 센서(Weight Sensor), 화물 잠금 상태(Cargo-Lock Status), 무게중심 추정(Center-of-Gravity Estimation), 화물칸 환경 및 적재 정보를 비행 전과 비행 중에 감시할 수 있다. 검증된 화물 정보는 비행 계획과 에너지 관리 시스템에서 사용할 수 있어야 하며, 항공기의 질량 및 균형 가정이 수동으로 입력된 물류 데이터에만 의존하지 않고 실제 탑재화물 구성과 일치하도록 해야 한다.

지상 통신(Ground Communication)은 기본적인 비행 안정성을 지속적인 연결에 의존하지 않으면서 명령, 감시, 임무 갱신 및 항공기 건전성 정보를 제공해야 한다. 주 데이터링크(Primary Datalink)가 상실되거나 성능이 저하되면 항공기가 불안정해지는 대신 사전에 정의된 자율 동작(Autonomous Behavior)이 실행되어야 한다. 운용 범위를 확보하기 위해 여러 통신 기술을 결합할 수 있으며, 핵심 명령 인터페이스에는 인증(Authentication), 무결성 검사(Integrity Checking), 암호화(Encryption), 접근 제어(Access Control) 및 비인가 제어 방지 기능이 필요하다.

항공전자 전력 분배(Avionics Power Distribution)는 에너지가 궁극적으로 동일한 항공기 에너지원에서 공급되더라도 주 추진 네트워크(Main Propulsion Network)로부터 독립성을 확보해야 한다. 절연형 직류 변환(Isolated DC/DC Conversion), 이중화된 저전압 버스(Redundant Low-Voltage Bus), 보호된 전원 공급선(Protected Feeder) 및 국부 백업 에너지(Local Backup Energy)를 통해 추진 버스에 이상이 발생해도 비행 컴퓨터, 항법 센서, 통신 장비 및 필수 액추에이터를 계속 운용할 수 있다. 전원 영역 분리(Power-Domain Separation)는 물리적 설치와 함께 고려하여 하나의 전기적 사고가 이중화된 항공전자 채널을 동시에 정지시키지 않도록 해야 한다.

열 설계(Thermal Design) 역시 컴퓨팅 신뢰성(Computing Reliability)에 중요하다. 비행 컴퓨터, 네트워크 스위치, 항법 프로세서, 통신 장비 및 고성능 임무 컴퓨터는 지속적으로 열을 발생시키며, 항공기는 광범위한 외기 온도와 고도 변화에 노출될 수 있다. 온도 감시와 핵심 채널을 위한 독립적인 냉각 설비를 통해 공통 열 고장(Common Thermal Failure)을 방지할 수 있다. 안전 필수 항공전자 장비가 열적 운용 한계에 접근하기 전에 임무 컴퓨팅의 성능을 선택적으로 제한(Derating)할 수 있어야 한다.

항공기는 지상관제소(Ground Station), 기단 시스템(Fleet System), 정비 도구, 물류 인프라 및 잠재적으로 교통관리 서비스(Traffic-Management Service)와 연결되므로 사이버보안(Cybersecurity)을 아키텍처에 통합해야 한다. 보안 부팅(Secure Boot), 인증된 소프트웨어, 보호된 통신, 통제된 업데이트 메커니즘, 네트워크 분할, 로깅(Logging) 및 접근 관리를 통해 비필수 인터페이스의 침해가 비행 필수 기능으로 확산될 가능성을 줄일 수 있다. 동시에 보안 메커니즘 자체가 결정론적이고 가용성이 높은 비행 운용을 저해해서는 안 된다.

궁극적으로 5톤급 화물 무인항공기의 항공전자 시스템(Avionics)은 하나의 중앙집중식 컴퓨터가 아니라 분산형(Distributed), 분할형(Partitioned), 이중화형(Redundant), 재구성 가능형(Reconfigurable) 시스템으로 설계해야 한다. 비행제어, 항법, 추진, 에너지, 통신, 화물, 건전성 관리 및 자율 기능은 기능적으로 구분된 상태를 유지하면서 통제된 인터페이스를 통해 검증된 정보를 교환한다. 이러한 아키텍처는 지역 물류 운용(Regional Logistics Operation)과 이후 절에서 다루는 인증 계획(Certification Planning)에 필요한 신뢰성 높은 컴퓨팅 기반을 제공한다.

## 10.04. Regional Logistics Interface

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

지역 물류 인터페이스(Regional Logistics Interface)는 5톤급 화물 무인항공기(Cargo UAV)가 운송 임무 전 과정에서 물류센터(Logistics Center), 버티포트(Vertiport), 창고(Warehouse), 기단 시스템(Fleet System), 지상 인프라(Ground Infrastructure), 공역 서비스(Airspace Service)와 상호작용하는 방식을 정의한다. 독립적인 항공기 인터페이스와 달리 물리적인 화물 이송, 디지털 화물 정보, 항공기 준비 상태, 항로 승인, 에너지 상태 및 운항 일정을 함께 조정해야 한다. 따라서 항공기는 독립적인 자율 이동체가 아니라 광범위한 지역 물류 네트워크(Regional Logistics Network)를 구성하는 하나의 노드(Node)가 된다.

일반적인 임무는 물류 관리 시스템(Logistics Management System)이 출발지, 목적지, 화물 질량, 크기, 우선순위, 배송 시간대 및 취급 요구조건을 포함하는 운송 요청(Transport Request)을 생성하면서 시작된다. 이 정보는 기단 관리 시스템(Fleet Management System)으로 전달되고, 시스템은 사용 가능한 항공기, 탑재 능력, 항속거리, 정비 상태, 에너지 예비량 및 기상 조건을 평가한다. 이후 적합한 무인항공기를 배정하고 임무 계획 시스템(Mission-Planning System)이 운용 가능한 비행계획을 생성할 수 있다.

창고 운영(Warehouse Operation)과 항공기 사이의 인터페이스는 수동 데이터 재입력(Manual Data Re-Entry)을 최소화해야 한다. 화물 식별자(Shipment Identifier), 화물 적하목록(Cargo Manifest), 위험 또는 민감 화물 분류, 목적지 정보 및 취급 지침을 화물 관리 시스템(Cargo Management System)에 디지털 방식으로 전달할 수 있다. 중량 센서와 화물 식별 장치는 실제 적재된 화물을 독립적으로 확인하며, 항공기는 출발 임무를 승인하기 전에 물리적 측정값과 물류 기록을 비교할 수 있다.

화물 적재(Cargo Loading)를 위해서는 무인항공기와 지상 물류 장비 사이에 표준화된 기계 및 전기 인터페이스(Standardized Mechanical and Electrical Interface)가 필요하다. 팔레트(Pallet), 컨테이너(Container), 자동 적재 플랫폼, 지게차 또는 로봇 화물 취급 시스템은 정의된 화물칸 크기, 체결 지점, 잠금 메커니즘 및 적재 한계에 맞게 연동되어야 한다. 이러한 표준화는 회전시간(Turnaround Time)을 줄이고 모든 목적지마다 전용 취급 장비를 설치하지 않고도 동일한 항공기가 여러 지역 물류 허브에서 운용될 수 있도록 한다.

화물 잠금 시스템(Cargo-Locking System)은 비행 전에 탑재화물이 기계적으로 확실하게 고정되었다는 정보를 제공해야 한다. 잠금 상태, 도어 상태, 측정된 화물 중량 및 추정 무게중심(Center of Gravity, CG)을 항공전자 및 임무 관리 시스템으로 전달할 수 있다. 측정된 구성이 허용 질량 또는 균형 한계를 초과하면 출발 승인을 차단해야 한다. 이를 통해 화물 적재를 독립적인 지상 작업으로 취급하는 대신 물류 처리 과정과 항공기 비행 안전을 직접 연결할 수 있다.

버티포트(Vertiport) 또는 물류 허브(Logistics Hub) 인프라는 항공기의 도착, 주기, 적재, 충전 또는 급유, 점검 및 출발을 조정해야 한다. 디지털 지상 인터페이스(Digital Ground Interface)를 통해 주기장 가용성, 착륙구역 상태, 에너지 서비스 준비 상태, 화물 취급 상태 및 예상 회전시간을 교환할 수 있다. 여러 화물 무인항공기가 동일한 시설의 제한된 착륙구역, 충전 장비, 연료 시스템, 정비 자원 및 적재 스테이션을 공유하는 경우 자동화된 일정 관리(Automated Scheduling)는 더욱 중요해진다.

에너지 서비스(Energy Servicing)는 5톤급 항공기의 하이브리드 전기 아키텍처(Hybrid-Electric Architecture)를 반영해야 한다. 지상 인프라는 회전 작업 중 배터리 충전, 연료 보급, 전기 진단 및 열 상태 조절(Thermal Conditioning)을 제공해야 할 수 있다. 항공기와 지상 시스템은 배터리 충전 상태(State of Charge, SOC), 요구 충전 에너지, 연료량, 예상 임무 에너지 요구량 및 출발 시간을 교환해야 한다. 이를 통해 모든 에너지원을 항상 최대 용량까지 충전하는 대신 다음 임무에 맞추어 에너지 서비스를 계획할 수 있다.

지역 운항(Regional Operation)을 위해서는 기단 관리(Fleet Management)와의 통합도 필요하다. 기단 시스템은 여러 항공기의 운용 상태를 관리하고 위치, 탑재 능력, 항속거리, 에너지 상태, 정비 상태 및 예상 가용성을 기반으로 임무를 배정할 수 있다. 하나의 항공기를 사용할 수 없게 되면 전체 물류 작업흐름(Logistics Workflow)을 다시 구성하지 않고 다른 기체를 재배정할 수 있다. 따라서 기단 수준 최적화(Fleet-Level Optimization)를 통해 항공기 활용률, 에너지 소비, 정비 주기, 화물 우선순위 및 인프라 혼잡도를 균형 있게 관리할 수 있다.

임무 계획(Mission Planning)은 물류 요청과 항공기의 물리적 한계를 연결한다. 항로 거리, 탑재화물 질량, 바람, 고도 프로파일, 공역 제한, 사용 가능한 착륙지, 연료량, 배터리 상태 및 예비 에너지 요구조건을 함께 평가해야 한다. 요청된 화물 운송은 항공기가 우회(Diversion), 체공(Holding), 복행(Go-Around), 시스템 성능 저하 및 대체 착륙을 위한 정의된 비상 여유도(Contingency Margin)를 유지하면서 항로를 완주할 수 있을 때만 실행 가능한 임무로 전환되어야 한다.

물류 인터페이스는 적용 가능한 경우 무인교통관리(Unmanned Traffic Management, UTM) 또는 유스페이스(U-Space) 서비스와도 정보를 교환해야 한다. 비행 의도(Flight Intent), 항로 정보, 식별 정보, 지오펜싱(Geofencing) 제약, 공역 제한 및 교통 정보는 출발 시간과 항로 선정에 영향을 줄 수 있다. 공역 가용성이 변경되면 기단 및 물류 시스템은 무인항공기가 출발하기 전이나 이미 운항 중인 상황에서도 도착 시간, 에너지 소비, 화물 일정 또는 항공기 배정을 다시 계산해야 할 수 있다.

비행 중 물류 시스템(Logistics System)이 안전 필수 항공전자 시스템(Safety-Critical Avionics)에 제한 없이 접근할 필요는 없다. 대신 통제된 인터페이스(Controlled Interface)를 통해 항공기 위치, 예상 도착시간(Estimated Time of Arrival, ETA), 임무 상태, 화물 상태, 에너지 여유도 및 주요 예외 상황과 같은 검증된 운용 정보를 제공해야 한다. 안전 필수 제어 기능은 항공기와 승인된 지휘 인프라 내부에 유지된다. 이러한 분리를 통해 고객 및 창고 시스템이 비행제어 네트워크에 불필요한 접근 경로를 만들지 않고도 화물 운송 상태를 추적할 수 있다.

지역 항공 물류(Regional Air Logistics)는 바람, 공역 제한, 항로 변경, 목적지 혼잡 및 항공기 성능의 영향을 받기 때문에 예상 도착시간(Estimated Time of Arrival)은 지속적으로 갱신되어야 한다. 갱신된 도착 예측 정보를 이용하면 목적지 시설이 착륙구역, 화물 취급 장비, 작업자, 자율 로봇(Autonomous Robot) 또는 후속 운송수단을 사전에 준비할 수 있다. 따라서 무인항공기는 비행 중 단순히 지리적 위치를 보고하는 것이 아니라 동기화된 물류 계획(Synchronized Logistics Planning)에 참여하게 된다.

온도 민감 화물, 파손 위험 화물, 의료 화물, 산업용 화물 또는 고가 화물의 경우 화물 상태 감시(Cargo Condition Monitoring)가 필요할 수 있다. 화물 관리 시스템은 온도, 습도, 진동, 충격, 도어 상태 또는 기타 응용 분야별 파라미터를 감시하고 이러한 측정값을 화물 기록과 연계할 수 있다. 비정상적인 상태는 물류 시스템에 보고할 수 있지만 비행 안전에 관련된 핵심 판단은 항공기의 안전 및 임무 관리 로직(Safety and Mission-Management Logic)에 의해 수행되어야 한다.

목적지에 도착하면 항공기는 공중 임무 제어(Airborne Mission Control)에서 협조된 지상 화물 처리(Coordinated Ground Handling) 상태로 전환되어야 한다. 착륙 확인, 주기 위치 배정, 추진 시스템 안전 상태, 화물 잠금 해제 승인 및 하역 준비 상태를 지상 인터페이스를 통해 교환할 수 있다. 화물은 항공기가 검증된 안전 상태에 도달한 이후에만 인계되어야 한다. 이후 디지털 배송 증명(Digital Proof of Delivery)을 통해 항공기 식별정보, 화물 식별정보, 도착 시간, 화물 상태 및 인계 상태를 물류 정보 시스템에 연계할 수 있다.

회전 효율(Turnaround Efficiency)은 지역 화물 운항의 중요한 경제적 요소가 된다. 항공기는 짧은 지상 체류시간 동안 화물을 하역하고 새로운 화물을 적재하며, 급유, 충전, 자동 건전성 점검(Automated Health Check), 임무 데이터 업로드 및 다음 항로 수신을 수행해야 할 수 있다. 표준화된 디지털 및 물리적 인터페이스를 적용하면 안전이 확보되는 범위에서 이러한 작업을 병렬로 수행할 수 있으며, 유휴시간을 줄이고 항공기 한 대가 하루 동안 수행할 수 있는 생산적인 임무 횟수를 증가시킬 수 있다.

궁극적으로 지역 물류 인터페이스(Regional Logistics Interface)는 화물 운송 수요, 기단 배정, 화물 취급, 항공기 임무 계획, 에너지 서비스, 공역 협조, 비행 수행, 목적지 준비 및 배송 확인을 하나의 종단간 연결(End-to-End Connection)로 통합해야 한다. 5톤급 화물 무인항공기에서 이러한 통합은 자율 비행 능력(Autonomous Flight Capability)을 실질적인 운송 서비스(Transportation Service)로 전환한다. 또한 이후 인증 계획(Certification Plan)에서 고려해야 하는 운용 인터페이스와 인증 근거 정보 흐름(Evidence Flow)의 기반을 제공한다.

## 10.05. 5t Certification Plan

![](images/image5.png){width="7.268055555555556in" height="7.268055555555556in"}

5톤급 화물 무인항공기(Cargo UAV)의 인증 계획(Certification Plan)은 추진, 항공전자, 구조, 화물 장비 및 자율 기능을 각각 독립적인 인증 항목으로 취급하기보다 항공기를 하나의 통합 항공 시스템(Integrated Airborne System)으로 다루어야 한다. 이 항공기는 상당한 질량, 고에너지 하이브리드 전기 추진(High-Energy Hybrid-Electric Propulsion), 자율 비행 능력 및 지역 물류 운용을 결합한다. 따라서 인증은 이러한 상호 연계 시스템이 정상, 비정상, 성능 저하 및 비상 운용 조건 전반에서 허용 가능한 안전성을 달성함을 입증해야 한다.

인증 계획(Certification Planning)은 인증을 위한 가정이 시스템 아키텍처에 직접적인 영향을 미치므로 항공기 개발 초기부터 시작해야 한다. 의도된 운용(Intended Operations), 최대이륙중량(Maximum Takeoff Mass), 탑재 한계, 비행영역(Flight Envelope), 운용 고도, 기상 조건, 자율화 수준, 지상통제 개념, 공역 환경 및 비상 절차가 인증 기준(Certification Basis)을 형성한다. 이러한 조건을 늦게 정의하면 이미 선정된 구조, 전자장치, 소프트웨어 또는 이중화 개념이 요구되는 안전 목표를 충족하지 못해 비용이 많이 드는 재설계가 필요할 수 있다.

시스템 수준 안전성 평가(System-Level Safety Assessment)는 인증 요구조건을 할당하는 기반을 제공한다. 항공기 기능을 분석하여 안전 비행 지속, 제어된 착륙, 지상의 사람, 화물 또는 주변 공역에 영향을 줄 수 있는 고장을 식별해야 한다. 이후 고장 상태(Failure Condition)를 심각도에 따라 분류하고, 이에 대응하는 무결성(Integrity) 및 보증 요구조건(Assurance Requirement)을 비행제어, 추진, 항법, 전력, 통신, 화물 및 지상 시스템 아키텍처에 하향 할당할 수 있다.

인증 과정은 항공기 수준 요구조건에서 서브시스템 요구조건, 구현, 검증 및 최종 증거(Evidence)까지 이어지는 추적성(Traceability)을 확립해야 한다. 각각의 안전 요구조건은 이를 충족하는 하드웨어, 소프트웨어, 인터페이스 또는 운용 절차와 연결되어야 한다. 이후 검증 결과를 통해 구현된 시스템이 최초 요구조건을 충족한다는 사실을 입증해야 한다. 이러한 추적성은 개발이 개념 설계에서 상세 엔지니어링 및 시험 단계로 진행되는 과정에서 중요한 안전 가정이 누락되는 것을 방지한다.

비행제어 인증(Flight-Control Certification)은 안정화, 유도, 항법, 액추에이터 제어 및 비행영역 보호(Flight-Envelope Protection)가 승인된 전체 운용영역에서 신뢰성 있게 유지된다는 증거를 요구한다. 이중화된 비행제어 컴퓨터(Flight Control Computer), 센서, 통신 경로 및 액추에이터는 정상 운용뿐 아니라 고장이 주입된 조건에서도 평가되어야 한다. 검증을 통해 위험한 과도응답(Unsafe Transient Response)을 발생시키지 않으면서 적절한 고장 감지, 격리, 보팅(Voting), 재구성, 성능 저하 제어 및 복구 동작이 수행됨을 입증해야 한다.

하이브리드 전기 추진 시스템(Hybrid-Electric Propulsion System)은 기존의 전력 분배를 넘어서는 인증 고려사항을 발생시킨다. 배터리, 연료 시스템, 발전기, 정류기(Rectifier), 고전압 버스, 인버터, 모터, 접촉기(Contactor) 및 열관리 장비가 긴밀하게 결합된 추진 체계를 구성한다. 인증 증거는 정의된 구성요소 고장이 발생했을 때 전기적 절연, 보호 협조(Protection Coordination), 열적 격리(Thermal Containment), 고장 차단, 에너지원 관리 및 충분한 잔여 추력(Remaining Thrust)이 확보됨을 입증해야 한다.

배터리 안전(Battery Safety)은 저장된 높은 전기에너지가 열적, 전기적 및 화재 위험을 발생시킬 수 있으므로 특별한 주의가 필요하다. 시험에서는 과전류, 과전압, 비정상 온도, 절연 고장, 충전 고장, 내부 또는 외부 고장 시나리오 및 격리·봉쇄 동작(Containment Behavior)을 평가해야 한다. 배터리 감시 시스템과 에너지 관리 시스템(Energy Management System, EMS)은 위험 상태를 감지하고 영향을 받은 영역을 격리하는 동시에, 시스템 아키텍처가 해당 초기 고장을 허용하도록 설계된 경우 필수 항공기 기능을 유지해야 한다.

항공전자 하드웨어 및 소프트웨어 보증(Avionics Hardware and Software Assurance)은 기능 구현 이후에 추가되는 것이 아니라 개발 수명주기(Development Lifecycle)에 통합되어야 한다. 비행 필수 컴퓨팅(Flight-Critical Computing)은 통제된 요구조건, 아키텍처, 구현, 검증, 형상 관리(Configuration Management) 및 변경 관리(Change Management)를 필요로 한다. 안전 기능에 사용되는 하드웨어와 소프트웨어는 할당된 중요도(Criticality)에 적합한 증거를 제공해야 한다. 비행 필수 기능과 임무 기능 사이의 파티셔닝(Partitioning)은 한 영역의 고장이나 과도한 자원 사용이 다른 영역을 손상시키지 않는다는 점도 입증해야 한다.

통신 아키텍처(Communication Architecture)는 결정론적 동작(Deterministic Behavior), 이중화, 데이터 무결성 및 고장 격리에 대한 인증 증거가 필요하다. 안전 필수 메시지(Safety-Critical Message)는 정의된 네트워크 부하와 고장 조건에서도 정해진 시간 한계 내에 목적지에 도달해야 한다. 이중화 링크는 스위치, 케이블, 인터페이스 및 전원 고장 조건에서 시험되어야 한다. 안전 필수, 임무, 정비, 화물 및 외부 통신 네트워크 사이의 게이트웨이(Gateway)는 의도된 기능적 분리(Functional Separation)를 유지해야 한다.

항법 인증(Navigation Certification)은 의도된 지역 운송 임무에 충분한 정확도(Accuracy), 무결성(Integrity), 연속성(Continuity) 및 가용성(Availability)을 입증해야 한다. 위성항법시스템(GNSS), 관성 센서, 대기자료원(Air-Data Source), 고도 측정 및 기타 항법 입력은 개별적으로 그리고 통합 센서 융합 시스템(Integrated Fusion System)으로 평가되어야 한다. 시험에는 성능이 저하되거나 사용할 수 없는 센서, 불일치하는 측정값, 통신 지연 및 환경 교란을 포함하여 항법 불확실성에 대한 항공기의 대응이 이해되고 제한된 범위 내에 있음을 입증해야 한다.

화물 시스템(Cargo System)의 동작이 항공기 안전에 영향을 줄 수 있는 경우 해당 시스템도 인증 범위에 포함된다. 탑재화물 중량, 무게중심(Center of Gravity, CG), 화물 잠금장치, 도어, 구조적 체결 지점 및 적재 인터페이스는 정의된 한계 내에서 유지되어야 한다. 안전하지 않은 적재 상태가 감지되면 항공기가 출발하지 못하도록 해야 한다. 또한 비행 하중, 진동, 기동, 착륙 조건 및 관련 비상 상황에서 화물 유지 성능을 평가하여 화물이 통제되지 않은 위험을 발생시키지 않는다는 점을 입증해야 한다.

지상통제 및 데이터링크 인증(Ground-Control and Datalink Certification)은 항공기의 자율 운항 특성을 반영해야 한다. 승인된 운용 개념에서 명시적으로 요구하지 않는 한 안전한 비행이 중단 없는 인간과의 통신에 의존해서는 안 된다. 데이터링크의 상실, 성능 저하, 지연, 데이터 손상 또는 비인가 사용이 발생하면 항공기는 정의된 동작을 수행해야 한다. 따라서 지상관제소(Ground Station), 명령 인터페이스, 인증 메커니즘 및 운용 절차가 항공기 운용에 영향을 줄 수 있는 경우 안전 논증(Safety Argument)의 일부가 된다.

사이버보안 보증(Cybersecurity Assurance)은 무인항공기를 지상관제소, 기단 관리(Fleet Management), 정비 시스템, 물류 네트워크, 소프트웨어 업데이트 메커니즘 및 교통관리 서비스와 연결하는 인터페이스를 다루어야 한다. 위협 분석(Threat Analysis)을 통해 안전 관련 기능에 영향을 줄 수 있는 경로를 식별해야 한다. 이후 보안 부팅(Secure Boot), 인증된 소프트웨어, 암호화 통신, 접근 제어, 네트워크 분할, 로깅(Logging) 및 통제된 정비 접근을 단순한 정보기술 기능이 아니라 전체 보증 체계(Assurance Framework)의 일부로 검증할 수 있다.

환경 적합성 검증(Environmental Qualification)은 탑재 장비가 실제 운용 중 예상되는 환경 조건에서도 계속 정상적으로 동작함을 입증해야 한다. 온도, 고도, 진동, 충격, 습도, 전자기 간섭(Electromagnetic Interference), 전원 과도현상(Power Transient) 및 기타 적용 가능한 환경 스트레스를 장비의 설치 위치와 기능에 따라 고려해야 한다. 실험실 벤치에서 정상적으로 작동하는 구성요소라도 항공기의 진동, 냉각 제한, 배선 영향 또는 전자기 결합(Electromagnetic Coupling)에 노출되면 다르게 동작할 수 있으므로 실제 설치 조건을 반영한 적합성 검증이 필요하다.

인증 시험(Certification Testing)은 구성요소와 서브시스템 검증에서 통합 항공기 시험으로 단계적으로 발전해야 한다. 하드웨어 인 더 루프 시뮬레이션(Hardware-in-the-Loop Simulation, HIL)을 이용하면 실제 비행 전에 비행 컴퓨터와 추진 제어기에 반복 가능한 정상 및 고장 시나리오를 적용할 수 있다. 지상 통합 시험(Ground Integration Test)을 통해 전체 전기, 통신, 열관리 및 화물 인터페이스를 검증할 수 있다. 이후 비행시험(Flight Testing)을 통해 운용영역을 점진적으로 확장하면서 성능, 조종 특성, 자율 기능, 고장 대응, 에너지 예비량 및 운용 절차를 통제된 조건에서 확인할 수 있다.

최종 인증 논증(Certification Argument)은 설계 증거, 안전성 분석, 검증 기록, 적합성 시험 결과, 지상시험, 비행시험, 형상 기록(Configuration Record), 정비 요구조건 및 운용 제한사항을 결합하여 규정 준수(Compliance)를 일관되게 입증해야 한다. 따라서 5톤급 화물 무인항공기의 인증은 요구조건, 아키텍처, 구현, 시험 및 운용을 연결하는 지속적인 엔지니어링 프로세스(Continuous Engineering Process)이다. 이러한 접근법은 하이브리드 전기 자율 화물 항공기(Hybrid-Electric Autonomous Cargo Aircraft)를 지역 물류 네트워크(Regional Logistics Network)에 실제 배치하기 위해 필요한 보증 기반(Assurance Foundation)을 확립한다.
