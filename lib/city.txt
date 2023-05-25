class CitiesByState {
  String? message;
  int? code;
  bool? success;
  String? sId;
  int? id;
  int? countryId;
  int? stateId;
  String? cityName;
  int? cityStatus;
  String? citySlug;

  CitiesByState({
    this.message,
    this.cityName,
    this.citySlug,
    this.cityStatus,
    this.countryId,
    this.id,
    this.sId,
    this.stateId,
    this.code,
    this.success,
  });

  CitiesByState.fromJson(Map<String, dynamic> json) {
    message = json['message'];
    sId = json['_id'];
    id = json['id'];
    countryId = json['country_id'];
    stateId = json['state_id'];
    cityName = json['city_name'];
    cityStatus = json['city_status'];
    citySlug = json['city_slug'];
    code = json['code'];
    success = json['success'];
  }

  Map<String, dynamic> toJson() {
    final Map<String, dynamic> data = <String, dynamic>{};
    data['message'] = message;
    data['_id'] = sId;
    data['id'] = id;
    data['country_id'] = countryId;
    data['state_id'] = stateId;
    data['city_name'] = cityName;
    data['city_status'] = cityStatus;
    data['city_slug'] = citySlug;
    data['code'] = code;
    data['success'] = success;
    return data;
  }
}
