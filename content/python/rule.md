
레이아웃 구조는 Designer, 동적 크기 조정은 코드"**로 나누는 게 정석


Designer에서 할 것

레이아웃 배치 (QVBoxLayout, QHBoxLayout, QGridLayout, QSplitter 등)
sizePolicy 설정 (Expanding, Fixed, Preferred 등) — 이게 핵심인데, 이것만 제대로 잡아두면 창 리사이즈될 때 위젯들이 알아서 비율대로 늘어나고 줄어듦
minimumSize / maximumSize 같은 제약조건
고정된 배치 구조 (예: sena의 A~H 헥사곤 배치처럼 "이 위젯은 여기, 저 위젯은 저기"라는 구조 자체)

이유는 간단해요. 레이아웃 구조를 코드로 짜면 나중에 위젯 하나 위치만 바꿔도 코드를 열어서 addWidget 호출 순서, row/col 인덱스 다 뒤져야 함. Designer는 드래그 앤 드롭으로 끝나고, .ui 파일이 XML이라 diff도 보기 편함.
코드로 할 것

런타임에 데이터에 따라 달라지는 크기 (예: file_manager의 파일 개수에 따라 리스트 높이 조절)
동적으로 위젯을 추가/제거하는 경우 (예: study_manager에서 카드 개수가 유동적일 때)
창 크기에 비선형적으로 반응해야 하는 특수 로직 (예: 창이 특정 너비 이하로 줄어들면 패널을 숨긴다든지)
splitter의 초기 비율 설정 (setSizes()) — Designer에서 splitter 자체는 만들되, 초기 비율은 showEvent나 초기화 코드에서 지정하는 게 실전에서 더 안정적임 (Designer에서 지정한 비율이 DPI나 폰트 설정에 따라 어긋나는 경우가 있음)