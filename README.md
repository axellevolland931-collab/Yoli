// mobile_app/lib/models/energy_model.dart (Дополнение)

// ... (FuelType, ConnectorType, PortStatus, HazardLevel, SearchMode, FuelPrice, ChargingPort - остаются прежними) ...

class RouteDetails {
  final Duration estimatedTravelTime; // ETA до станции
  final double distanceKm;
  
  RouteDetails({required this.estimatedTravelTime, required this.distanceKm});
}

class UnifiedStation {
  // ... (id, name, brand, latitude, longitude, fuelPrices, chargingPorts, hazardLevel - остаются прежними) ...
  
  // Новые поля для рейтингов и маршрута
  final double overallQualityScore; // 0.0 - 10.0: Комплайнс, Сервис, Актуальность
  final RouteDetails? routeInfo; // Информация о маршруте до станции
  
  // Добавляем прогноз доступности портов (для EV)
  final double predictivePortAvailability; // Вероятность, что порт будет свободен к ETA (0.0 - 1.0)

  UnifiedStation({
    // ... (Обязательные поля) ...
    this.overallQualityScore = 0.0,
    this.routeInfo,
    this.predictivePortAvailability = 0.0,
  });

  UnifiedStation copyWith({
    List<FuelPrice>? fuelPrices, 
    List<ChargingPort>? chargingPorts,
    double? overallQualityScore,
    RouteDetails? routeInfo,
    double? predictivePortAvailability,
  }) {
    return UnifiedStation(
      id: id, name: name, brand: brand, latitude: latitude, longitude: longitude, 
      fuelPrices: fuelPrices ?? this.fuelPrices,
      chargingPorts: chargingPorts ?? this.chargingPorts,
      hazardLevel: hazardLevel,
      overallQualityScore: overallQualityScore ?? this.overallQualityScore,
      routeInfo: routeInfo ?? this.routeInfo,
      predictivePortAvailability: predictivePortAvailability ?? this.predictivePortAvailability,
    );
  }
}
