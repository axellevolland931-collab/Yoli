// mobile_app/lib/models/fuel_model.dart (Дополнение)
// ... (FuelType, ServiceType, HazardLevel, FuelPrice, HazardScore - остаются прежними) ...

enum CrowdLevel { empty, moderate, busy, full }

class DynamicStationData {
  final CrowdLevel crowdLevel;
  final Duration estimatedWaitTime; // Время ожидания у колонки
  final double priceChangeProbability; // Вероятность изменения цены в ближайший час (0.0 - 1.0)
  
  DynamicStationData({
    required this.crowdLevel,
    required this.estimatedWaitTime,
    this.priceChangeProbability = 0.0,
  });
}

class FuelStation {
  // ... (id, name, brand, latitude, longitude, prices, services, hazardCompliance - остаются прежними) ...
  final DynamicStationData? dynamicData; // Динамические данные о загруженности и прогнозе

  FuelStation({
    // ... (Обязательные поля) ...
    this.dynamicData,
  });

  // copyWith для обновления динамического состояния (цены, очереди, прогноз)
  FuelStation copyWith({List<FuelPrice>? prices, DynamicStationData? dynamicData}) {
    return FuelStation(
      id: id, name: name, brand: brand, latitude: latitude, longitude: longitude, 
      prices: prices ?? this.prices, services: services, 
      hazardCompliance: hazardCompliance,
      dynamicData: dynamicData ?? this.dynamicData,
    );
  }
}
// ... (FuelFilters остается прежним) ...
