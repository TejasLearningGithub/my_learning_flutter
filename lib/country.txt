class IndiaCountryModal {
  String? message;
  String? sId;
  int? countryId;
  String? countryCode;
  String? countryName;
  
  int? code;
  bool? success;

  IndiaCountryModal({this.message, this.sId,this.countryCode,this.countryId,this.countryName ,this.code, this.success});

  IndiaCountryModal.fromJson(Map<String, dynamic> json) {
    message = json['message'];
    sId = json['_id'];
    countryId = json['country_id'];
    countryCode = json['country_code'];
    countryName = json['country_name'];
    code = json['code'];
    success = json['success'];
  }

  Map<String, dynamic> toJson() {
    final Map<String, dynamic> data = <String, dynamic>{};
    data['message'] = message;
    data['_id'] = sId;
    data['country_id'] = countryId;
    data['country_code'] = countryCode;
    data['country_name'] = countryName;
    data['code'] = code;
    data['success'] = success;
    return data;
  }
}

