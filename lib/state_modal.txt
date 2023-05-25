class StateByCountryId {
  String? message;
  int? stateId;
  int? code;
  bool? success;
  String? sId;
  int? id;
  int? countryId;
  String? stateName;
  String? stateCode;

  StateByCountryId(
      {this.message,
      this.sId,
      this.countryId,
      this.id,
      this.stateCode,
      this.stateName,
      this.code,
      this.success,
      this.stateId});

  StateByCountryId.fromJson(Map<String, dynamic> json) {
    message = json['message'];
    sId = json['_id'];
    id = json['id'];
    countryId = json['country_id'];
    stateName = json['state_name'];
    stateCode = json['state_code'];
    code = json['code'];
    success = json['success'];
    stateId = json['state_id'] ?? 0;
  }

  Map<String, dynamic> toJson() {
    final Map<String, dynamic> data = <String, dynamic>{};
    data['message'] = message;
    data['_id'] = sId;
    data['id'] = id;
    data['country_id'] = countryId;
    data['state_name'] = stateName;
    data['state_code'] = stateCode;
    data['code'] = code;
    data['success'] = success;
    data['state_id'] = stateId;
    return data;
  }
}
